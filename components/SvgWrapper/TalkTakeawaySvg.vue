<script setup lang="ts">
import SvgElementFilter from '../SvgElementFilter.vue'
import mySvgContent from '/assets/excalidraw-drawings/talk-overview/talk-overview-8_light.svg?raw'
</script>

<template>
  <SvgElementFilter
    display-indices="all"
    svg-class="w-full"
    :svg-content="mySvgContent"
  />
</template>
