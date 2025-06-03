<script setup lang="ts">
import { useNav } from '@slidev/client'
import { computed } from 'vue'
import SvgElementFilter from '../SvgElementFilter.vue'
// import mySvgContent from '/assets/example.svg?raw'

const { clicks } = useNav()

const elementsToShow = computed<number[] | 'all'>(() => {
  if (clicks.value >= 9) {
    return 'all'
  }

  let res: number[] = []
  if (clicks.value >= 1) {
    res = [...res, 0, 1, 2, 12]
  }
  if (clicks.value >= 2) {
    res = [...res, 0, 1, 2, 3, 4, 7, 14, 16]
  }
  if (clicks.value >= 3) {
    res = [...res, 19, 20]
  }
  if (clicks.value >= 4) {
    res = [...res, 6, 8]
  }
  if (clicks.value >= 5) {
    res = [...res, 5, 10]
  }
  if (clicks.value >= 6) {
    res = [...res, 9, 11]
  }
  if (clicks.value >= 7) {
    res = [...res, 13, 17, 21]
  }
  if (clicks.value >= 8) {
    res = [...res, 15, 18]
  }
  if (clicks.value >= 9) {
    res = [...res, 22, 23]
  }
  return res
})
</script>

<template>
  <!-- <SvgElementFilter
    :display-indices="elementsToShow"
    svg-class="w-full"
    :svg-content="mySvgContent"
  /> -->
</template>
