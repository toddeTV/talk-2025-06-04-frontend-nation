<script setup lang="ts">
import sdk from '@stackblitz/sdk'
import { onMounted } from 'vue'

const props = withDefaults(defineProps<{
  projectId: string // The StackBlitz project ID to embed.
  domElementId?: string // The ID or class of the element where the StackBlitz project will be embedded.
  forceEmbedLayout?: boolean
  hideExplorer?: boolean
  hideNavigation?: boolean
  clickToLoad?: boolean
  showSidebar?: boolean
  openFile?: string | string[]
  theme?: 'light' | 'dark' | 'default'
  view?: 'default' | 'editor' | 'preview'
}>(), {
  clickToLoad: false,
  domElementId: `stackblitz-embed-${Math.random().toString(36).substring(2, 15)}`, // Default to a random string
  forceEmbedLayout: true,
  hideExplorer: false,
  hideNavigation: false,
  openFile: 'README.md',
  showSidebar: false,
  theme: 'light',
  view: 'default',
})

onMounted(() => {
  sdk.embedProjectId(
    props.domElementId,
    props.projectId,
    {
      // crossOriginIsolated: true,
      clickToLoad: props.clickToLoad,
      forceEmbedLayout: props.forceEmbedLayout,
      hideExplorer: props.hideExplorer,
      hideNavigation: props.hideNavigation,
      openFile: props.openFile,
      showSidebar: props.showSidebar,
      theme: props.theme,
      view: props.view,
    },
  )
})
</script>

<template>
  <div
    :id="props.domElementId"
    class="h-full w-full"
  />
</template>
