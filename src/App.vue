<template>
  <nav
    class="bg-white text black dark:bg-gray-800 dark:text-white shadow-lg transition-color duration-300"
  >
    <div
      class="max-w-screen-xl flex flex-wrap items-center justify-between mx-auto p-4"
    >
      <div>Vue-Tree-Drag</div>
      <div class="flex flex-row items-center space-x-6">
        <label
          class="inline-flex items-center cursor-pointer p-1 bg-gray-200 rounded-full w-14 h-8 dark:bg-gray-600"
        >
          <input
            type="checkbox"
            :value="theme === 'light'"
            class="sr-only peer"
            @change="toggleTheme"
          />
          <span
            class="absolute h-6 w-6 p-1 rounded-full bg-white transition-all duration-300 peer-checked:translate-x-6 peer-checked:opacity-0 peer-checked:rotate-90 peer-checked:bg-gray-800 peer-checked:fill-white"
          >
            <svg
              class="w-full h-full"
              xmlns="http://www.w3.org/2000/svg"
              height="1em"
              viewBox="0 0 512 512"
            >
              <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
              <path
                d="M375.7 19.7c-1.5-8-6.9-14.7-14.4-17.8s-16.1-2.2-22.8 2.4L256 61.1 173.5 4.2c-6.7-4.6-15.3-5.5-22.8-2.4s-12.9 9.8-14.4 17.8l-18.1 98.5L19.7 136.3c-8 1.5-14.7 6.9-17.8 14.4s-2.2 16.1 2.4 22.8L61.1 256 4.2 338.5c-4.6 6.7-5.5 15.3-2.4 22.8s9.8 13 17.8 14.4l98.5 18.1 18.1 98.5c1.5 8 6.9 14.7 14.4 17.8s16.1 2.2 22.8-2.4L256 450.9l82.5 56.9c6.7 4.6 15.3 5.5 22.8 2.4s12.9-9.8 14.4-17.8l18.1-98.5 98.5-18.1c8-1.5 14.7-6.9 17.8-14.4s2.2-16.1-2.4-22.8L450.9 256l56.9-82.5c4.6-6.7 5.5-15.3 2.4-22.8s-9.8-12.9-17.8-14.4l-98.5-18.1L375.7 19.7zM269.6 110l65.6-45.2 14.4 78.3c1.8 9.8 9.5 17.5 19.3 19.3l78.3 14.4L402 242.4c-5.7 8.2-5.7 19 0 27.2l45.2 65.6-78.3 14.4c-9.8 1.8-17.5 9.5-19.3 19.3l-14.4 78.3L269.6 402c-8.2-5.7-19-5.7-27.2 0l-65.6 45.2-14.4-78.3c-1.8-9.8-9.5-17.5-19.3-19.3L64.8 335.2 110 269.6c5.7-8.2 5.7-19 0-27.2L64.8 176.8l78.3-14.4c9.8-1.8 17.5-9.5 19.3-19.3l14.4-78.3L242.4 110c8.2 5.7 19 5.7 27.2 0zM256 368a112 112 0 1 0 0-224 112 112 0 1 0 0 224zM192 256a64 64 0 1 1 128 0 64 64 0 1 1 -128 0z"
              />
            </svg>
          </span>
          <span
            class="absolute h-6 w-6 p-1 rounded-full bg-white transition-all duration-300 translate-x-0 opacity-0 -rotate-90 peer-checked:translate-x-6 peer-checked:opacity-100 peer-checked:rotate-0 peer-checked:bg-gray-800 peer-checked:fill-white"
          >
            <svg
              class="w-full h-full"
              xmlns="http://www.w3.org/2000/svg"
              height="1em"
              viewBox="0 0 384 512"
            >
              <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
              <path
                d="M144.7 98.7c-21 34.1-33.1 74.3-33.1 117.3c0 98 62.8 181.4 150.4 211.7c-12.4 2.8-25.3 4.3-38.6 4.3C126.6 432 48 353.3 48 256c0-68.9 39.4-128.4 96.8-157.3zm62.1-66C91.1 41.2 0 137.9 0 256C0 379.7 100 480 223.5 480c47.8 0 92-15 128.4-40.6c1.9-1.3 3.7-2.7 5.5-4c4.8-3.6 9.4-7.4 13.9-11.4c2.7-2.4 5.3-4.8 7.9-7.3c5-4.9 6.3-12.5 3.1-18.7s-10.1-9.7-17-8.5c-3.7 .6-7.4 1.2-11.1 1.6c-5 .5-10.1 .9-15.3 1c-1.2 0-2.5 0-3.7 0c-.1 0-.2 0-.3 0c-96.8-.2-175.2-78.9-175.2-176c0-54.8 24.9-103.7 64.1-136c1-.9 2.1-1.7 3.2-2.6c4-3.2 8.2-6.2 12.5-9c3.1-2 6.3-4 9.6-5.8c6.1-3.5 9.2-10.5 7.7-17.3s-7.3-11.9-14.3-12.5c-3.6-.3-7.1-.5-10.7-.6c-2.7-.1-5.5-.1-8.2-.1c-3.3 0-6.5 .1-9.8 .2c-2.3 .1-4.6 .2-6.9 .4z"
              />
            </svg>
          </span>
        </label>
        <a
          href="https://github.com/ttnhan95"
          class="w-6 h-6 fill-black dark:fill-white"
        >
          <svg
            class="w-full h-full"
            xmlns="http://www.w3.org/2000/svg"
            height="1em"
            viewBox="0 0 496 512"
          >
            <!--! Font Awesome Free 6.4.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2023 Fonticons, Inc. -->
            <path
              d="M165.9 397.4c0 2-2.3 3.6-5.2 3.6-3.3.3-5.6-1.3-5.6-3.6 0-2 2.3-3.6 5.2-3.6 3-.3 5.6 1.3 5.6 3.6zm-31.1-4.5c-.7 2 1.3 4.3 4.3 4.9 2.6 1 5.6 0 6.2-2s-1.3-4.3-4.3-5.2c-2.6-.7-5.5.3-6.2 2.3zm44.2-1.7c-2.9.7-4.9 2.6-4.6 4.9.3 2 2.9 3.3 5.9 2.6 2.9-.7 4.9-2.6 4.6-4.6-.3-1.9-3-3.2-5.9-2.9zM244.8 8C106.1 8 0 113.3 0 252c0 110.9 69.8 205.8 169.5 239.2 12.8 2.3 17.3-5.6 17.3-12.1 0-6.2-.3-40.4-.3-61.4 0 0-70 15-84.7-29.8 0 0-11.4-29.1-27.8-36.6 0 0-22.9-15.7 1.6-15.4 0 0 24.9 2 38.6 25.8 21.9 38.6 58.6 27.5 72.9 20.9 2.3-16 8.8-27.1 16-33.7-55.9-6.2-112.3-14.3-112.3-110.5 0-27.5 7.6-41.3 23.6-58.9-2.6-6.5-11.1-33.3 2.6-67.9 20.9-6.5 69 27 69 27 20-5.6 41.5-8.5 62.8-8.5s42.8 2.9 62.8 8.5c0 0 48.1-33.6 69-27 13.7 34.7 5.2 61.4 2.6 67.9 16 17.7 25.8 31.5 25.8 58.9 0 96.5-58.9 104.2-114.8 110.5 9.2 7.9 17 22.9 17 46.4 0 33.7-.3 75.4-.3 83.6 0 6.5 4.6 14.4 17.3 12.1C428.2 457.8 496 362.9 496 252 496 113.3 383.5 8 244.8 8zM97.2 352.9c-1.3 1-1 3.3.7 5.2 1.6 1.6 3.9 2.3 5.2 1 1.3-1 1-3.3-.7-5.2-1.6-1.6-3.9-2.3-5.2-1zm-10.8-8.1c-.7 1.3.3 2.9 2.3 3.9 1.6 1 3.6.7 4.3-.7.7-1.3-.3-2.9-2.3-3.9-2-.6-3.6-.3-4.3.7zm32.4 35.6c-1.6 1.3-1 4.3 1.3 6.2 2.3 2.3 5.2 2.6 6.5 1 1.3-1.3.7-4.3-1.3-6.2-2.2-2.3-5.2-2.6-6.5-1zm-11.4-14.7c-1.6 1-1.6 3.6 0 5.9 1.6 2.3 4.3 3.3 5.6 2.3 1.6-1.3 1.6-3.9 0-6.2-1.4-2.3-4-3.3-5.6-2z"
            />
          </svg>
        </a>
      </div>
    </div>
  </nav>
  <div class="p-20 dark:bg-gray-600">
  <div class="flex flex-col gap-10">
      <div class="flex gap-10 items-center">
        <img src="@/assets/img/json.svg" class="h-[80px] dark:fill-white" />
        <svg height="4em" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc. --><path d="M438.6 150.6c12.5-12.5 12.5-32.8 0-45.3l-96-96c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L338.7 96 32 96C14.3 96 0 110.3 0 128s14.3 32 32 32l306.7 0-41.4 41.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l96-96zm-333.3 352c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L109.3 416 416 416c17.7 0 32-14.3 32-32s-14.3-32-32-32l-306.7 0 41.4-41.4c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0l-96 96c-12.5 12.5-12.5 32.8 0 45.3l96 96z"/></svg>
        <img src="@/assets/img/treeview.svg" class="h-[80px] dark:fill-white" />
      </div>
      <form>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6 items-center max-w-sm w-full">
          <label
            for="tree-title-field"
            class="block text-sm font-medium text-black dark:text-white "
            >Title Field</label
          >
          <input
            type="text"
            id="tree-title-field"
            class="bg-gray-100 border border-gray-200 text-black text-sm rounded-lg block w-full p-2.5 dark:bg-gray-600 dark:border-gray-400 dark:placeholder-gray-400 dark:text-white"
            v-model="tree.titleField"
          />
        </div>
        <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mb-6 items-center max-w-sm w-full">
          <label
            for="tree-children-field"
            class="block text-sm font-medium text-black dark:text-white"
            >Children Field</label
          >
          <input
            type="text"
            id="tree-children-field"
            class="bg-gray-100 border border-gray-200 text-black text-sm rounded-lg block w-full p-2.5 dark:bg-gray-600 dark:border-gray-400 dark:placeholder-gray-400 dark:text-white"
            v-model="tree.childrenField"
          />
        </div>
      </form>
    </div>
  <div class="grid grid-cols-1 md:grid-cols-2 gap-20 h-max">
    <div class="flex flex-col min-h-[60vh]">
      <h3 class="flex text-lg font-semibold uppercase p-4">
          Raw Data
      </h3>
      <div
        class="w-full px-4 py-2 bg-gray-200 rounded-t-xl dark:border-gray-600 dark:bg-gray-700 text-xs flex justify-between border dark:border-gray-400"
      >
        <div class="flex items-center gap-2">
          <button class="border-2 border-gray-600 p-1 bg-white" @click="beautifyJson">
            <svg class="w-full h-full" height="1.5em" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc. -->
              <path d="M0 64C0 46.3 14.3 32 32 32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32C14.3 96 0 81.7 0 64zM192 192c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H224c-17.7 0-32-14.3-32-32zm32 96H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H224c-17.7 0-32-14.3-32-32s14.3-32 32-32zM0 448c0-17.7 14.3-32 32-32H416c17.7 0 32 14.3 32 32s-14.3 32-32 32H32c-17.7 0-32-14.3-32-32zM127.8 268.6L25.8 347.9C15.3 356.1 0 348.6 0 335.3V176.7c0-13.3 15.3-20.8 25.8-12.6l101.9 79.3c8.2 6.4 8.2 18.9 0 25.3z"/></svg>
          </button>
          <button class="border-2 border-gray-600 p-1 bg-white" @click="copyJson">
            <svg class="w-full h-full" height="1.5em" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc. -->
              <path d="M208 0H332.1c12.7 0 24.9 5.1 33.9 14.1l67.9 67.9c9 9 14.1 21.2 14.1 33.9V336c0 26.5-21.5 48-48 48H208c-26.5 0-48-21.5-48-48V48c0-26.5 21.5-48 48-48zM48 128h80v64H64V448H256V416h64v48c0 26.5-21.5 48-48 48H48c-26.5 0-48-21.5-48-48V176c0-26.5 21.5-48 48-48z"/></svg>
          </button>
        </div>  
      </div>
      <textarea class="w-full h-full p-4 text-sm shadow-lg rounded-b-xl dark:bg-gray-600 border dark:border-gray-400 dark:text-white" v-model="displayData"></textarea>
    </div>
    
  <div class="flex flex-col min-h-[60vh]">
    <h3 class="flex text-lg font-semibold uppercase p-4">Tree Data</h3>
      <div
        class="w-full px-4 py-2 bg-gray-200 rounded-t-xl dark:border-gray-600 dark:bg-gray-700 text-xs flex justify-between border dark:border-gray-400"
      >
        <div class="flex items-center gap-2">
          <button class="border-2 border-gray-600 p-1 bg-white" @click="addNode">
            <svg class="w-full h-full" height="1.5em" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512"><!--!Font Awesome Free 6.5.2 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc. --><path d="M256 80c0-17.7-14.3-32-32-32s-32 14.3-32 32V224H48c-17.7 0-32 14.3-32 32s14.3 32 32 32H192V432c0 17.7 14.3 32 32 32s32-14.3 32-32V288H400c17.7 0 32-14.3 32-32s-14.3-32-32-32H256V80z"/></svg>
          </button>
        </div>
      </div>
      <vue-tree-drag
        :model-value="inputData"
        :item-name-field="tree.titleField"
        :item-child-field="tree.childrenField"
        :draggable="true"
        :editable="true"
        :deletable="true"
        :data-change="dataUpdate"
        class="p-6 rounded-b-xl shadow-lg h-full border dark:border-gray-400"
      />
    </div>
  </div>
</div>
</template>

<script setup>
import { reactive, ref, watch } from "vue";
import VueTreeDrag from "@/components/tree/VueTreeDrag.vue";

const theme = ref("light");
const displayData = ref('')

const inputData = ref([
]);

const tree = reactive({
  titleField: "name",
  childrenField: "children",
});

const toggleTheme = () => {
  theme.value = theme.value === "light" ? "dark" : "light";
  if (theme.value == "dark") {
    document.querySelector("body").classList.add("dark");
  } else {
    document.querySelector("body").classList.remove("dark");
  }
};


const dataUpdate = () => {
  displayData.value = JSON.stringify(inputData.value, null, 4)
}

const copyJson = () => {
  navigator.clipboard.writeText(displayData.value)
}

const beautifyJson = () => {
  displayData.value = JSON.stringify(inputData.value, null, 4)
}

const addNode = () => {
  inputData.value.push({
    name: "New Node",
    data: "New Data",
    children: [],
  })
}

watch(displayData, () => {
  inputData.value = JSON.parse(displayData.value)
})
</script>
