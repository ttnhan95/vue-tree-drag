<template>
  <li
    v-if="item.isPlaceholder"
    class="placeholder border-dashed border-2 border-gray-400 rounded mb-1"
    :style="{ height: item.height + 'px' }"
    @dragover.stop.prevent="onPlaceholderDragOver($event, this)"
    @drop="onDrop($event, this)"
  ></li>
  <li
    v-else
    class="relative"
    :draggable="draggable"
    @dragstart.stop="onDragStart($event, this)"
    @dragend.stop="onDragEnd($event)"
    @dragover.stop="onDragOver($event, this)"
    @dragenter.stop="onDragEnter"
  >
    <div
      class="text-gray-900 bg-gray-100 hover:bg-gray-200 hover:shadow border border-gray-200 shadow rounded mb-1 divide-y-2 divide-gray-200 hover:divide-gray-100"
    >
      <div class="flex items-center p-3 text-sm font-bold space-x-4 py-3 px-5">
        <button
          v-if="hasChild"
          class="flex pointer-events-auto items-center transition-all duration-300"
          @click="toggleChildren"
          :class="[childrenShow ? 'rotate-90' : 'rotate-0']"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            height="1em"
            viewBox="0 0 320 512"
          >
            <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
            <path
              d="M310.6 233.4c12.5 12.5 12.5 32.8 0 45.3l-192 192c-12.5 12.5-32.8 12.5-45.3 0s-12.5-32.8 0-45.3L242.7 256 73.4 86.6c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0l192 192z"
            />
          </svg>
        </button>
        <span class="flex-grow">
          {{ item[itemNameField] }}
        </span>
        <span class="flex gap-4">
          <button class="flex" @click="toggleView" v-if="!onView">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="1em"
              viewBox="0 0 576 512"
            >
              <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
              <path
                d="M288 80c-65.2 0-118.8 29.6-159.9 67.7C89.6 183.5 63 226 49.4 256c13.6 30 40.2 72.5 78.6 108.3C169.2 402.4 222.8 432 288 432s118.8-29.6 159.9-67.7C486.4 328.5 513 286 526.6 256c-13.6-30-40.2-72.5-78.6-108.3C406.8 109.6 353.2 80 288 80zM95.4 112.6C142.5 68.8 207.2 32 288 32s145.5 36.8 192.6 80.6c46.8 43.5 78.1 95.4 93 131.1c3.3 7.9 3.3 16.7 0 24.6c-14.9 35.7-46.2 87.7-93 131.1C433.5 443.2 368.8 480 288 480s-145.5-36.8-192.6-80.6C48.6 356 17.3 304 2.5 268.3c-3.3-7.9-3.3-16.7 0-24.6C17.3 208 48.6 156 95.4 112.6zM288 336c44.2 0 80-35.8 80-80s-35.8-80-80-80c-.7 0-1.3 0-2 0c1.3 5.1 2 10.5 2 16c0 35.3-28.7 64-64 64c-5.5 0-10.9-.7-16-2c0 .7 0 1.3 0 2c0 44.2 35.8 80 80 80zm0-208a128 128 0 1 1 0 256 128 128 0 1 1 0-256z"
              />
            </svg>
          </button>
          <button class="flex" @click="toggleView" v-else>
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="1em"
              viewBox="0 0 640 512"
            >
              <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
              <path
                d="M38.8 5.1C28.4-3.1 13.3-1.2 5.1 9.2S-1.2 34.7 9.2 42.9l592 464c10.4 8.2 25.5 6.3 33.7-4.1s6.3-25.5-4.1-33.7L525.6 386.7c39.6-40.6 66.4-86.1 79.9-118.4c3.3-7.9 3.3-16.7 0-24.6c-14.9-35.7-46.2-87.7-93-131.1C465.5 68.8 400.8 32 320 32c-68.2 0-125 26.3-169.3 60.8L38.8 5.1zm151 118.3C226 97.7 269.5 80 320 80c65.2 0 118.8 29.6 159.9 67.7C518.4 183.5 545 226 558.6 256c-12.6 28-36.6 66.8-70.9 100.9l-53.8-42.2c9.1-17.6 14.2-37.5 14.2-58.7c0-70.7-57.3-128-128-128c-32.2 0-61.7 11.9-84.2 31.5l-46.1-36.1zM394.9 284.2l-81.5-63.9c4.2-8.5 6.6-18.2 6.6-28.3c0-5.5-.7-10.9-2-16c.7 0 1.3 0 2 0c44.2 0 80 35.8 80 80c0 9.9-1.8 19.4-5.1 28.2zm9.4 130.3C378.8 425.4 350.7 432 320 432c-65.2 0-118.8-29.6-159.9-67.7C121.6 328.5 95 286 81.4 256c8.3-18.4 21.5-41.5 39.4-64.8L83.1 161.5C60.3 191.2 44 220.8 34.5 243.7c-3.3 7.9-3.3 16.7 0 24.6c14.9 35.7 46.2 87.7 93 131.1C174.5 443.2 239.2 480 320 480c47.8 0 89.9-12.9 126.2-32.5l-41.9-33zM192 256c0 70.7 57.3 128 128 128c13.3 0 26.1-2 38.2-5.8L302 334c-23.5-5.4-43.1-21.2-53.7-42.3l-56.1-44.2c-.2 2.8-.3 5.6-.3 8.5z"
              />
            </svg>
          </button>
          <button class="flex" v-if="deletable" @click="removeNode($event)">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              height="1em"
              viewBox="0 0 448 512"
            >
              <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
              <path
                d="M135.2 17.7L128 32H32C14.3 32 0 46.3 0 64S14.3 96 32 96H416c17.7 0 32-14.3 32-32s-14.3-32-32-32H320l-7.2-14.3C307.4 6.8 296.3 0 284.2 0H163.8c-12.1 0-23.2 6.8-28.6 17.7zM416 128H32L53.2 467c1.6 25.3 22.6 45 47.9 45H346.9c25.3 0 46.3-19.7 47.9-45L416 128z"
              />
            </svg>
          </button>
        </span>
      </div>

      <transition
        enter-from-class="grid-rows-[0fr]"
        enter-to-class="grid-rows-[1fr]"
        leave-from-class="grid-rows-[1fr]"
        leave-to-class="grid-rows-[0fr]"
      >
        <div v-if="onView" class="grid transition-all duration-300 ease-out">
          <div class="overflow-hidden text-sm font-medium px-3">
            <div class="grid grid-cols-3 gap-2 flex m-2" v-for="k in attrKeys">
              <div class="col-span-1 flex flex-start items-center">
                {{ k }}:
              </div>
              <div class="flex-start col-span-2">
                <span v-if="!editable" class="flex">
                  {{ item[k] }}
                </span>
                <input
                  v-else-if="typeof item[k] === 'string'"
                  type="text"
                  class="w-full bg-transparent py-2 pl-1 text-gray-800 placeholder:text-gray-400 focus:ring-0 focus:bg-white focus:border-gray-400 focus:border-gray-400"
                  v-model="item[k]"
                />
                <input
                  v-else-if="typeof item[k] === 'number'"
                  type="number"
                  class="w-full bg-transparent py-2 pl-1 text-gray-800 placeholder:text-gray-400 focus:ring-0 focus:bg-white focus:border-gray-400 focus:border-gray-400"
                  v-model="item[k]"
                />
                <span v-else-if="typeof item[k] === 'boolean'" class="flex">
                  <label class="flex">
                    {{ item[k] }}
                    <input type="checkbox" class="hidden" v-model="item[k]" />
                  </label>
                </span>
                <span v-else class="items-center"> {{ item[k] }} </span>
              </div>
            </div>
          </div>
        </div>
      </transition>
    </div>
    <transition
      enter-from-class="grid-rows-[0fr]"
      enter-to-class="grid-rows-[1fr]"
      leave-from-class="grid-rows-[1fr]"
      leave-to-class="grid-rows-[0fr]"
    >
      <div
        v-if="childrenShow"
        class="grid transition-all duration-300 ease-out"
        :style="{ 'margin-left': levelIndent + 'px' }"
      >
        <ul class="w-full overflow-hidden">
          <tree-node
            v-for="(child, i) in item[itemChildField]"
            :item="child"
            :draggable="draggable"
            :editable="editable"
            :deletable="deletable"
            :on-drag-start="onDragStart"
            :on-drag-end="onDragEnd"
            :on-drag-over="onDragOver"
            :on-placeholder-drag-over="onPlaceholderDragOver"
            :on-drop="onDrop"
            :parent="item[itemChildField]"
            :level-indent="levelIndent"
            :grand-parent="parent"
            :parent-node="item"
            :prev-child="
              i >= 1 ? item[itemChildField][i - 1][itemChildField] : []
            "
            :item-name-field="itemNameField"
            :item-child-field="itemChildField"
          />
        </ul>
      </div>
    </transition>
  </li>
</template>

<script setup>
import { ref, computed } from "vue";
import emitter from "@/utils/emitter";

const props = defineProps({
  item: {
    type: Object,
    default: {},
  },
  draggable: {
    type: Boolean,
  },
  parent: {
    type: Array,
  },
  grandParent: {
    type: Array,
  },
  parentNode: {
    type: Object,
  },
  prevChild: {
    type: Object,
  },
  editable: {
    type: Boolean,
  },
  deletable: {
    type: Boolean,
  },
  itemChildField: {
    type: String,
    default: "children",
  },
  itemNameField: {
    type: String,
    default: "name",
  },
  onDragStart: {
    type: Function,
    default: () => false,
  },
  onDragEnd: {
    type: Function,
    default: () => false,
  },
  onDragOver: {
    type: Function,
    default: () => false,
  },
  onPlaceholderDragOver: {
    type: Function,
    default: () => false,
  },
  onDrop: {
    type: Function,
    default: () => false,
  },
  levelIndent: {
    type: Number,
    required: true,
  },
  deleteAction: {
    type: Function,
    default: () => false,
  },
});

const childrenShow = ref(true);
const onView = ref(false);

const toggleChildren = () => {
  childrenShow.value = !childrenShow.value;
};

const toggleView = () => {
  onView.value = !onView.value;
};

const onDragEnter = () => {
  childrenShow.value = true;
};

const removeNode = (e) => {
  let deleteIndex = Array.prototype.indexOf.call(props.parent, props.item);
  props.parent.splice(deleteIndex, 1);
  emitter.emit('data-change')
};

const hasChild = computed(() => {
  return !!(
    props.item[props.itemChildField] &&
    props.item[props.itemChildField].length > 0
  );
});

const attrKeys = computed(() => {
  return Object.keys(props.item);
});
</script>
