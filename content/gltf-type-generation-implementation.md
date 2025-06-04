---
layout: basic
---

# glTF type generation - Implementation

<v-clicks>

- <ant-design-frown-filled class="text-red-400" /> `three.js` is for runtime, especially the loaders (only in browser, not in node runtime)
  - <ant-design-smile-filled class="text-green-400" /> solution: patch and implement it as a clone to also still have the original GLTFLoader
- run `three.js` in node dev and pipe model into it, we then get the runtime object
  - <ant-design-smile-filled class="text-green-400" /> No own parsing
  - <ant-design-smile-filled class="text-green-400" /> Exact what the user gets when they load the model in their runtime
- generate types out of the runtime object by taking the names of all children
- store scene graph paths with the child indices linked to the child names
- use handlebars to generate files
- we generate:
  ```diff
   @/assets/models/Train.gltf
   @/assets/models/Train.bin
   @/assets/models/Train-texture1.png
   @/assets/models/Train-texture2.png
  +@/assets/models/Train.gltf.d.ts      <- the typing
  +@/assets/models/Train.gltf.js        <- actual code with node get helper function and model graph representation
  ```

</v-clicks>
