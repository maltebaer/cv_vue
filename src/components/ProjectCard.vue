<template>
  <h4
    class="text-lg flex items-center space-x-2 cursor-pointer"
    @click="showContent = !showContent"
  >
    <ChevronDownIcon class="w-4 h-4 stroke-2" v-if="!showContent" />
    <ChevronUpIcon class="w-4 h-4 stroke-2" v-else />
    <span>{{ name }}</span>
  </h4>
  <div v-if="showContent">
    <img class="mt-2 border" :src="preview" :alt="name" />
    <p class="mt-2">{{ description }}</p>
  </div>
  <ul class="mt-2 flex flex-wrap">
    <li
      class="border border-blue-500 px-2 mr-1 my-1 rounded-lg text-blue-500 font-semibold text-sm cursor-default hover:bg-blue-500 hover:text-white"
      v-for="tool in technologies"
      :key="tool"
    >
      {{ tool }}
    </li>
  </ul>
</template>

<script lang="ts">
import {defineComponent, ref} from "vue";

import ChevronDownIcon from "./icons/ChevronDown.vue";
import ChevronUpIcon from "./icons/ChevronUp.vue";

export default defineComponent({
  name: "ProjectCard",
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
  components: {ChevronDownIcon, ChevronUpIcon},

  setup(props) {
    const {homepage, name, preview, description, technologies} = props.project;

    const showContent = ref<boolean>(false);

    return {homepage, name, preview, description, technologies, showContent};
  },
});
</script>
