<script setup lang="ts">
import { useNav } from '@slidev/client'
import { computed } from 'vue'
import SvgElementFilter from '../SvgElementFilter.vue'
import mySvgContent1 from '/assets/excalidraw-drawings/talk-overview/talk-overview-1_light.svg?raw'
import mySvgContent2 from '/assets/excalidraw-drawings/talk-overview/talk-overview-2_light.svg?raw'
import mySvgContent3 from '/assets/excalidraw-drawings/talk-overview/talk-overview-3_light.svg?raw'
import mySvgContent4 from '/assets/excalidraw-drawings/talk-overview/talk-overview-4_light.svg?raw'
import mySvgContent5 from '/assets/excalidraw-drawings/talk-overview/talk-overview-5_light.svg?raw'
import mySvgContent6 from '/assets/excalidraw-drawings/talk-overview/talk-overview-6_light.svg?raw'
import mySvgContent7 from '/assets/excalidraw-drawings/talk-overview/talk-overview-7_light.svg?raw'
import mySvgContent8 from '/assets/excalidraw-drawings/talk-overview/talk-overview-8_light.svg?raw'

const { clicks } = useNav()

const mySvgContent = computed(() => {
  switch (clicks.value) {
    case 1:
      return mySvgContent1
    case 2:
      return mySvgContent2
    case 3:
      return mySvgContent3
    case 4:
      return mySvgContent4
    case 5:
      return mySvgContent5
    case 6:
      return mySvgContent6
    case 7:
      return mySvgContent7
    case 8:
      return mySvgContent8
    default:
      return undefined
  }
})
</script>

<template>
  <SvgElementFilter
    v-if="mySvgContent"
    display-indices="all"
    svg-class="w-full"
    :svg-content="mySvgContent"
  />
</template>
