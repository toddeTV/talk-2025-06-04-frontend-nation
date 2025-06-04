---
layout: two-cols
---

# glTF example

::left::

<WindowWrapper background="#F5F5F5" height="body">
````md magic-move {lines: true}
```json {*}
{
    asset: {},
    scenes: [],
    nodes: [],
    materials: [],
    meshes: [],
    textures: [],
    images: [],
    accessors: [],
    bufferViews: [],
    samplers: [],
    buffers: [],
    animations: []
}
```
```json {3-14}
{
    asset: {},
    scenes: [
      {
        "extras":{
        },
        "name":"TrainScene",
        "nodes":[
          0,
          1,
          42,
        ]
      }
    ],
    nodes: [],
    materials: [],
    meshes: [],
    textures: [],
    images: [],
    accessors: [],
    bufferViews: [],
    samplers: [],
    buffers: [],
    animations: []
}
```
```json {4-19}
{
    asset: {},
    scenes: [],
    nodes: [
      {
        "mesh":4,
        "name":"Train",
        "scale":[
          150,
          1,
          150
        ],
        "translation":[
          0,
          -15,
          0
        ]
      }
    ],
    materials: [],
    meshes: [],
    textures: [],
    images: [],
    accessors: [],
    bufferViews: [],
    samplers: [],
    buffers: [],
    animations: []
}
```
```json {6-23}
{
    asset: {},
    scenes: [],
    nodes: [],
    materials: [],
    meshes: [
      {
        "name":"pantograph",
        "primitives":[
          {
            "attributes":{
              "POSITION":0,
              "NORMAL":1,
              "TEXCOORD_0":2
            },
            "extensions":{},
            "indices":3,
            "material":0,
            "mode":4
          }
        ]
      },
    ],
    textures: [],
    images: [],
    accessors: [],
    bufferViews: [],
    samplers: [],
    buffers: [],
    animations: []
}
```
```json {8-12,16-21}
{
    asset: {},
    scenes: [],
    nodes: [],
    materials: [],
    meshes: [],
    textures: [],
    images: [
      {
        "uri": "TrainTexture01.png"
      }
    ],
    accessors: [],
    bufferViews: [],
    samplers: [],
    buffers: [
      {
        "uri": "TrainModel.bin",
        "byteLength": 612368
      }
    ],
    animations: []
}
```
````
</WindowWrapper>

::right::

## Object Hierarchy

<div class="w-full h-[470px] flex justify-center items-center absolute left-0 top-16 -z-10">
  <GltfObjectHierarchyGraphSvg class="h-[470px]" />
</div>

<!-- dummy only to force the click count on this slide manually -->
<!-- <div v-click="8" /> -->

<div
  class="absolute top-36 left-196 w-15 h-7"
  v-mark="{ at: [1,2], color: '#26ab7a', type: 'box' }"
/>
<div
  class="absolute top-52 left-196 w-15 h-7"
  v-mark="{ at: [2,3], color: '#26ab7a', type: 'box' }"
/>
<div
  class="absolute top-70 left-196 w-15 h-7"
  v-mark="{ at: [3,4], color: '#26ab7a', type: 'box' }"
/>
<div
  class="absolute top-120 left-196 w-15 h-7"
  v-mark="{ at: [4,5], color: '#26ab7a', type: 'box' }"
/>
<div
  class="absolute top-120 left-164 w-15 h-7"
  v-mark="{ at: [4,5], color: '#26ab7a', type: 'box' }"
/>

<div
  v-click="6"
  class="absolute right-40 bottom-16 baseColor font-bold"
>
How do we load & use this?
</div>

<!--
... defines the scene graph
-->
