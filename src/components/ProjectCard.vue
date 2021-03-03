<template>
  <h3 class="text-xl font-semibold text-gray-500 flex items-center space-x-2">
    <span>{{ name }}</span>
  </h3>
  <ul class="mt-2 flex flex-wrap items-center">
    <li class="pr-2">
      <a :href="github" target="_blank">
        <GitHubIcon class="w-5 h-5 stroke-2 text-blue-500" />
      </a>
    </li>
    <li
      class="border border-blue-500 px-2 mr-1 my-1 rounded-lg text-blue-500 font-semibold text-sm cursor-default hover:bg-blue-500 hover:text-white"
      v-for="tool in technologies"
      :key="tool"
    >
      {{ tool }}
    </li>
  </ul>
  <a :href="homepage" target="_blank">
    <img class="mt-2 border" :src="preview" :alt="name" />
  </a>
  <p class="mt-2">{{ description }}</p>
</template>

<script lang="ts">
import {defineComponent} from "vue";

import GlobeIcon from "./icons/Globe.vue";
import GitHubIcon from "./icons/GitHub.vue";

export default defineComponent({
  name: "ProjectCard",
  props: {
    project: {
      type: Object,
      required: true,
    },
  },
  components: {GlobeIcon, GitHubIcon},

  setup(props) {
    const {
      homepage,
      name,
      preview,
      description,
      technologies,
      github,
    } = props.project;

    return {homepage, name, preview, description, technologies, github};
  },
});
</script>
