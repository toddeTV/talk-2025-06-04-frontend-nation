---
layout: basic
---

# glTF type generation - generated Example

<div class="flex flex-row gap-4 w-screen">
<div class="overflow-hidden !w-140">

````md magic-move {lines: true}
```ts {*}
// Train.gltf.d.ts
import type { Group, Mesh } from 'three'

declare const path: unique symbol

export const TrainScene: {
  [path]: [0]
  train: {
    [path]: [0, 0]
    roof: {
      [path]: [0, 0, 0]
      pantograph: {
        [path]: [0, 0, 0, 0]
      }
    }
  }
}

export function getNode(spec: typeof TrainScene): Promise<Group>
export function getNode(spec: typeof TrainScene.train): Promise<Group>
export function getNode(spec: typeof TrainScene.train.roof): Promise<Group>
export function getNode(spec: typeof TrainScene.train.roof.pantograph):
  Promise<Mesh>

export {}
```
````

</div>
<div class="overflow-hidden !w-95">

````md magic-move {lines: true}
```ts {*}
// Train.gltf.js
import gltfLoader from '[default or custom]'
import gltfPath from './Train.gltf'
const path = Symbol()

export const TrainScene = {
  [path]: [0],
  train: {
    [path]: [0, 0],
    roof: {
      [path]: [0, 0, 0],
      pantograph: {
        [path]: [0, 0, 0, 0],
      },
    },
  },
}
export async function getNode(spec) {
  let node =
    { children: (await loadModel()).scenes }
  for (const idx of spec[path]) {
    node = node.children[idx]
  }
  return node
}
async function loadModel() {
  return await gltfLoader.loadAsync(gltfPath)
}
```
````

</div>
</div>
