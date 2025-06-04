---
layout: basic
---

<h1 class="-mt-0.5">glTF - What the <mdi:duck class="color-yellow-600" /> ?</h1>

<VClicks at="1">

- File format to store 3D data (scenes, models, material, etc.)
- Main format for 3D data used in the web

</VClicks>

<div class="w-full h-8">
</div>

<div
    v-click="3"
    class="flex flex-row justify-center items-center w-full"
>
    <span class="text-2xl mr-2">glTF 1.0</span> <span class="text-md mr-2 color-gray-500">(2015)</span>
</div>

<Arrow
    v-click="4"
    v-bind="{ x1:500, y1:240, x2:500, y2:300, color: '#000000' }"
/>

<div
    v-click="4"
    class="flex flex-row justify-center items-center w-full mt-20"
>
    <span class="text-2xl mr-2">glTF 2.0</span> <span class="text-md mr-2 color-gray-500">(2017)</span>
</div>

<Arrow
    v-click="5"
    v-bind="{ x1:480, y1:350, x2:250, y2:420, color: '#000000' }"
/>
<Arrow
    v-click="6"
    v-bind="{ x1:500, y1:350, x2:500, y2:420, color: '#000000' }"
/>
<Arrow
    v-click="7"
    v-bind="{ x1:520, y1:350, x2:750, y2:420, color: '#000000' }"
/>

<div class="flex flex-row justify-between w-full gap-0">
    <div
        v-click="5"
        class="flex-grow-0 flex-shrink-0 flex flex-col justify-start items-start w-75 mt-20"
    >
        <div class="text-2xl mr-2">glTF 2.0 Seperated</div>
        <div>
            <ul>
                <li><code>.gltf</code> as JSON meta file</li>
                <li><code>.bin</code> as binary encoded buffers</li>
                <li>textures as images (<code>jpg</code>, <code>png</code>, ...)</li>
            </ul>
        </div>
    </div>
    <div
        v-click="6"
        class="flex-grow-0 flex-shrink-0 flex flex-col justify-start items-start w-55 mt-20"
    >
        <div class="text-2xl mr-2">glTF 2.0 Embedded</div>
        <div>
            One <code>.gltf</code> file as JSON. Assets are base64 encoded <code>data:</code> sources in <code>uri</code> fields.
        </div>
    </div>
    <div
        v-click="7"
        class="flex-grow-0 flex-shrink-0 flex flex-col justify-start items-start w-73 mt-20"
    >
        <div class="text-2xl mr-2">glTF 2.0 Binary</div>
        <div>
            <ul>
                <li>One binary encoded <code>.glb</code> file</li>
                <li>[optional] references external files</li>
            </ul>
        </div>
    </div>
</div>
