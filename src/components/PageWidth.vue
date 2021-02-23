<template>
  <div
    class="fixed top-0 z-10 h-12 w-full px-4 bg-gray-800 opacity-30 flex justify-start items-center"
  >
    <h1 class="font-mono text-white text-center">
      {{ width }} px ({{ breakpoint }})
    </h1>
  </div>
</template>

<script lang="ts">
import {defineComponent, computed} from "vue";
import {useWindowSize} from "@vueuse/core";

export default defineComponent({
  name: "PageWidth",

  setup() {
    const {width} = useWindowSize();

    const breakpoint = computed(() => {
      const innerWidth = width.value;

      if (innerWidth < 640) {
        return "none";
      } else if (innerWidth < 768) {
        return "sm";
      } else if (innerWidth < 1024) {
        return "md";
      } else if (innerWidth < 1280) {
        return "lg";
      } else if (innerWidth < 1536) {
        return "xl";
      } else {
        return "2xl";
      }
    });

    return {width, breakpoint};
  },
});
</script>
