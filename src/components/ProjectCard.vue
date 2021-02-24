<template>
  <a :href="homepage">{{ name }}</a>
  <img class="border" :src="preview" :alt="name" />
</template>

<script lang="ts">
import {defineComponent, computed} from "vue";

export default defineComponent({
  name: "ProjectCard",
  props: {
    project: Object,
  },

  setup(props) {
    const {homepage, name, preview} = props.project;
    return {homepage, name, preview};
  },
});
</script>
