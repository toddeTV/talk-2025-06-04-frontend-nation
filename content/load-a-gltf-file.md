---
layout: two-cols
---

# load a glTF file

::left::

## ThreeJS native

````md magic-move {lines: true}
```ts {*}
const loader = new GLTFLoader();

// loader.setDRACOLoader(dracoLoader);   <- optional

loader.load(
  '//localhost:3000/models/Island.gltf',
  function ( gltf ) { // on success
        // do something ...
    scene.add( gltf.scene );
    gltf.animations; // Array<THREE.AnimationClip>
    gltf.scene; // THREE.Group
    gltf.scenes; // Array<THREE.Group>
    gltf.cameras; // Array<THREE.Camera>
    gltf.asset; // Object
  },
  function ( xhr ) { // while loading
        const per = xhr.loaded / xhr.total * 100;
    console.log( per + '% loaded' );
  },
  function ( error ) { // on error
    console.log( 'An error happened' );
  }
);
```
````

::right::

<div v-click>

## Vision

````md magic-move {lines: true}
```ts {*}
// Pseudo Code

import { TrainGltf } from '@/assets/TrainGltf.gltf.js'

const trainModel = await TrainGltf

// do something with the model, e.g.

trainModel.windowLeft.opacity = 0.5
  // ^? three.Group

trainModel.windowLeft.opacity = 0.5
            // ^? three.Mesh
```
````

</div>
