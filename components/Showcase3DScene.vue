<script setup lang="ts">
import type { TresCanvasProps } from '@tresjs/core/dist/src/components/TresCanvas.vue.js'
import type {
  Object3D,
} from 'three'
import { GLTFModel, OrbitControls } from '@tresjs/cientos'
import { TresCanvas } from '@tresjs/core'
import { EffectComposerPmndrs, PixelationPmndrs } from '@tresjs/post-processing'
import {
  AmbientLight,
  CameraHelper,
  DirectionalLight,
  NoToneMapping,
  PerspectiveCamera,
  SRGBColorSpace,
  VSMShadowMap,
} from 'three'
import { ref, shallowRef, watch, watchEffect } from 'vue'

const showGrid = ref(false)
const showLights = ref(false)
const directionalLightRange = ref('140')
const showPlane = ref(false)
const showShadow = ref(false)
const showModel = ref(true)
const showInteraction = ref(false)
const showPostprocessing = ref(false)

const canvasProps = ref<TresCanvasProps>({
  alpha: false,
  clearColor: '#82DBC5',
  outputColorSpace: SRGBColorSpace,
  renderMode: 'always',
  // resize: true, // not present? hmm ... documentation says it's there and important for resizable canvas - weird
  // `VSMShadowMap` better shadows, but more performance heavy; `BasicShadowMap` is faster but has less quality
  shadowMapType: VSMShadowMap, // BasicShadowMap | PCFShadowMap | PCFSoftShadowMap | VSMShadowMap
  shadows: true,
  toneMapping: NoToneMapping,
  useLegacyLights: false,
})

// camera
const perspectiveCamera = new PerspectiveCamera()
perspectiveCamera.position.set(-5, 5, -2)
perspectiveCamera.near = 2
perspectiveCamera.far = 10
const perspectiveCameraHelper = new CameraHelper(perspectiveCamera)
const cameraRef = shallowRef()
watch(cameraRef, (value) => {
  if (!value) {
    return
  }
  value.add(perspectiveCameraHelper)
}, {
  immediate: true,
})
setInterval(() => {
  perspectiveCamera.lookAt(0, 0, 0)
}, 1000)

// lights
const lightsRef = shallowRef()
const lightsHelperRef = shallowRef()
watchEffect(() => {
  if (!lightsRef.value) {
    return
  }
  lightsRef.value.remove(...lightsRef.value.children)
  const ambientLight = new AmbientLight(0xFFFFFF, 0)
  ambientLight.intensity = 0.5
  const directionalLight = new DirectionalLight(0xFFFFFF, 0)
  directionalLight.castShadow = true
  directionalLight.intensity = 1.2
  directionalLight.shadow.camera.near = 5
  directionalLight.shadow.camera.far = +directionalLightRange.value / 10
  directionalLight.shadow.camera.left = -5
  directionalLight.shadow.camera.right = 5
  directionalLight.shadow.camera.top = 5
  directionalLight.shadow.camera.bottom = -5
  // directionalLight.shadow.camera.position.set(0, 3, 7)
  // directionalLight.shadow.camera.lookAt(0, 0, 0)
  directionalLight.position.set(7, 4, 7)
  directionalLight.target.position.set(0, 1, 0)
  // directionalLight.shadow.camera.updateProjectionMatrix()
  directionalLight.shadow.mapSize.width = 1024 * 2 // more beautiful, but performance heavier
  directionalLight.shadow.mapSize.height = 1024 * 2
  directionalLight.shadow.bias = -0.005 // fine tune to reduce shadow artifacts (negative and as close to 0 as possible)

  const directionalLightHelper = new CameraHelper(directionalLight.shadow.camera)
  lightsRef.value.add(ambientLight)
  lightsRef.value.add(directionalLight)
  if (lightsHelperRef.value) {
    lightsHelperRef.value.remove(...lightsHelperRef.value.children)
    lightsHelperRef.value.add(directionalLightHelper)
  }
})

// models
const modelRef = shallowRef<Object3D>()
// watch(modelRef, (model) => {
//   if(!model) {
//     return
//   }
//   console.dir(model)
//   model.position.set(100, 0, 0)
// }, {
//   immediate: true,
// })
const clickedKey = ref()
const timeout = ref()
function modelClicked(e) {
  if (!showInteraction.value) {
    return
  }
  // console.log(e.object.name)
  clickedKey.value = `"${e.object.name}" clicked`
  clearTimeout(timeout.value)
  timeout.value = setTimeout(() => {
    clickedKey.value = ''
  }, 3000)
}

// postprocessing
const pixelStrength = ref(10)

// TODO fix correctly
// fix: workaround bc model does not throw shadow if model is enabled before shadow
const { pause, resume } = watch([showModel, showShadow], ([model, shadow]) => {
  if (!(shadow === true && model === true)) {
    return
  }
  try {
    pause()
  }
  catch {
    // do nothing
  }
  showModel.value = false
  setTimeout(() => {
    showModel.value = true
    resume()
  }, 200)
}, {
  immediate: true,
})
</script>

<template>
  <WindowWrapper
    background="#E1F4FF"
    height="body"
  >
    <TresCanvas
      v-bind="canvasProps"
      class="absolute inset-0"
      clear-color="#E1F4FF"
    >
      <TresPerspectiveCamera
        :position="[-4, 4, 2]"
      />
      <OrbitControls
        :target="[0, 0.7, 0]"
      />

      <!-- world -->
      <TresGridHelper v-if="showGrid" />
      <TresAxesHelper v-if="showGrid" />

      <!-- lights -->
      <TresGroup
        ref="lightsRef"
      />
      <TresGroup
        v-if="showLights"
        ref="lightsHelperRef"
      />

      <!-- meshes -->
      <TresMesh
        v-if="showPlane"
        :position="[0, -0.01, 0]"
        :receive-shadow="showShadow"
        :rotation="[-Math.PI / 2, 0, 0]"
      >
        <TresPlaneGeometry :args="[10, 10, 10]" />
        <TresMeshToonMaterial color="#fefefe" />
      </TresMesh>

      <!-- 12: models -->
      <Suspense
        v-if="showModel"
      >
        <GLTFModel
          ref="modelRef"
          :cast-shadow="showShadow"
          path="/assets/models-3d/train-tram-round.glb"
          :receive-shadow="showShadow"
          :scale="1"
          @click="modelClicked"
        />
      </Suspense>

      <Suspense
        v-if="showPostprocessing"
      >
        <EffectComposerPmndrs>
          <PixelationPmndrs :granularity="+pixelStrength" />
        </EffectComposerPmndrs>
      </Suspense>
    </TresCanvas>

    <div class="absolute bottom-0 left-0 w-full z-2 flex flex-row justify-start pl-1">
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showGrid }"
        @click="showGrid = !showGrid"
      >
        Grid
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showLights }"
        @click="showLights = !showLights"
      >
        Lights
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showPlane }"
        @click="showPlane = !showPlane"
      >
        Plane
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showShadow }"
        @click="showShadow = !showShadow"
      >
        Shadow
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showModel }"
        @click="showModel = !showModel"
      >
        Model
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showInteraction }"
        @click="showInteraction = !showInteraction"
      >
        Interaction
      </div>
      <div
        class="cursor-pointer text-xs text-gray-500 p-1 select-none"
        :class="{ 'text-decoration-line': !showPostprocessing }"
        @click="showPostprocessing = !showPostprocessing"
      >
        Postprocessing
      </div>
    </div>
  </WindowWrapper>

  <input
    v-model="directionalLightRange"
    class="cursor-pointer w-20 absolute -bottom-5 left-25"
    max="180"
    min="60"
    type="range"
  >
  <input
    v-model="pixelStrength"
    class="cursor-pointer w-20 absolute -bottom-5 left-70"
    max="30"
    min="0"
    type="range"
  >

  <div
    v-if="clickedKey && showInteraction"
    class="absolute bottom-5 -left-50 w-60 text-center bg-baseColor text-white rounded-lg p-1 rotate-[-10deg]"
  >
    {{ clickedKey }}
  </div>
</template>
