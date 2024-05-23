<template>
  <ul>
    <tree-node
      v-for="(item, i) in modelValue"
      :item="item"
      :draggable="draggable"
      :editable="editable"
      :deletable="deletable"
      :on-drag-start="onDragStart"
      :on-drag-end="onDragEnd"
      :on-drag-over="onDragOver"
      :on-placeholder-drag-over="onPlaceholderDragOver"
      :on-drop="onDrop"
      :parent="modelValue"
      :level-indent="levelIndent"
      :prev-child="i >= 1 ? modelValue[i - 1][itemChildField] : []"
      :item-name-field="itemNameField"
      :item-child-field="itemChildField"
    />
  </ul>
</template>

<script setup>
import { onMounted } from 'vue'
import treeNode from "@/components/tree/TreeNode.vue";
import emitter from "@/utils/emitter";

const props = defineProps({
  modelValue: {
    type: Object,
    default: {},
  },
  draggable: {
    type: Boolean,
    default: true,
  },
  editable: {
    type: Boolean,
    default: false,
  },
  deletable: {
    type: Boolean,
    default: false,
  },
  itemChildField: {
    type: String,
    default: "children",
  },
  itemNameField: {
    type: String,
    default: "name",
  },
  placehoderClass: {
    type: String,
    default: "placeholder rounded-lg border-dashed border-2 border-gray-400",
  },
  dataChange: {
    type: Function,
    default: () => false,
  },
  levelIndent: {
    type: Number,
    default: 60,
  },
});

let dragItem;
let placeholder;
let placeholderItem;

const onDragStart = (e, srcNode) => {
  if (!srcNode.draggable) {
    return;
  }
  const dragRect = e.target.getBoundingClientRect();
  placeholder = {};
  placeholder.isPlaceholder = true;
  placeholder.height = dragRect.height - 4;

  let dragIndex = Array.prototype.indexOf.call(srcNode.parent, srcNode.item);

  dragItem = {
    item: srcNode.item,
    parent: srcNode.parent,
    index: dragIndex,
  };

  setTimeout(() => {
    srcNode.parent.splice(dragIndex, 1, placeholder);

    placeholderItem = {
      parent: srcNode.parent,
      index: dragIndex,
      padding: e.x - dragRect.x,
      grandParent: srcNode.grandParent,
    };
  }, 0);
};

const onDragEnd = (e) => {
  placeholderItem.parent.splice(placeholderItem.index, 1, dragItem.item);
};

const onDragOver = (e, srcNode) => {
  if (!placeholderItem) {
    return;
  }
  removePlaceholder(placeholderItem.parent);

  if (
    e.y <
    e.target.getBoundingClientRect().top +
      e.target.getBoundingClientRect().height / 2
  ) {
    let dragIndex = Array.prototype.indexOf.call(srcNode.parent, srcNode.item);
    srcNode.parent.splice(dragIndex, 0, placeholder);
    placeholderItem.parent = srcNode.parent;
    placeholderItem.index = dragIndex;
    placeholderItem.grandParent = srcNode.grandParent;
    placeholderItem.prevParent = srcNode.parent;
  } else {
    let dragIndex =
      Array.prototype.indexOf.call(srcNode.parent, srcNode.item) + 1;
    srcNode.parent.splice(dragIndex, 0, placeholder);
    placeholderItem.parent = srcNode.parent;
    placeholderItem.index = dragIndex;
    placeholderItem.grandParent = srcNode.grandParent;
    placeholderItem.prevParent = srcNode.parent;
  }
};

const onPlaceholderDragOver = (e, srcNode) => {
  if (e.x - placeholderItem.padding < e.target.getBoundingClientRect().x) {
    if (
      placeholderItem.index + 1 == placeholderItem.parent.length &&
      srcNode.grandParent &&
      srcNode.grandParent.length > 0
    ) {
      let placeIndex =
        Array.prototype.indexOf.call(srcNode.grandParent, srcNode.parentNode) +
        1;
      srcNode.grandParent.splice(placeIndex, 0, placeholder);
      removePlaceholder(placeholderItem.parent);
      placeholderItem.parent = srcNode.grandParent;
      placeholderItem.index = placeIndex;
    }
  } else if (
    e.x - placeholderItem.padding >
    e.target.getBoundingClientRect().x + props.levelIndent
  ) {
    if (placeholderItem.index > 0) {
      if (!srcNode.prevChild) {
        return;
      }
      srcNode.prevChild.push(placeholder);
      removePlaceholder(placeholderItem.parent);

      placeholderItem.parent = srcNode.prevChild;
      placeholderItem.index = srcNode.prevChild.length - 1;
    }
  }
};

const onDrop = (e) => {
  placeholderItem.parent.splice(placeholderItem.index, 1, dragItem.item);
  emitter.emit('data-change')
};

const removePlaceholder = (container) => {
  container.forEach(function (node, index) {
    if (node.isPlaceholder) {
      container.splice(index, 1);
    }
  });
};

onMounted(() => {
  emitter.on("data-change", props.dataChange);
});
</script>
