---
layout: basic
---

<h1>
    <simple-icons:unjs class="baseColor mr-2" />UnJs/Unplugin - our challenges with integrating
</h1>

<VClicks class="mt-7" :depth="2">

- <ant-design-frown-filled class="text-red-400" /> esbuild does only allow watching files during specific phases of the build process

  - this limits the watch benefits for esbuild as it might not detect added/ updated models

- <ant-design-frown-filled class="text-red-400" /> `emitFiles` does not provide a way to retrieve the generated filename.

  - reason is that for some bundler implementations this simply writes a file into the out dir (see esbuild)
  - solution is to simply generate fixed filenames that bundlers take without modifications

- <ant-design-frown-filled class="text-red-400" /> no unified way to detect dev/serve VS build
  - solution: custom checks for the bundlers which have this distinction and where it is possible to detect this

</VClicks>

<div class="flex justify-center mt-20 baseColor font-bold text-xl" v-click>
  The Build Tools are different and unifying them is not easy!
</div>
