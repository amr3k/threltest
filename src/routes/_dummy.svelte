<script lang="ts">
  import { GLTF } from "threlte";
  import { useGltfAnimations } from "$lib/threlte/useGltfAnimations";

  const { gltf, actions } = useGltfAnimations<"Confused">(({ actions }) => {
    // Either play your animations as soon as they are loaded
    // actions['Take 001']?.play();
    // console.log(actions);
  });

  // Or play them whenever you need
  const triggerAnimation = () => {
    console.log("click");
    // actions["Take 001"]?.play();
  };
  const pointerenter = () => {
    document.body.style.cursor = "pointer";
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
  };
</script>

<GLTF
  url={"/girl.glb"}
  position={{ x: 2, y: 1.32, z: 0 }}
  scale={{ x: 0.01, y: 0.01, z: 0.01 }}
  rotation={{ y: -90 * (Math.PI / 180) }}
  dracoDecoderPath="https://www.gstatic.com/draco/v1/decoders/"
  castShadow
  receiveShadow
  interactive
  bind:gltf={$gltf}
  on:click={triggerAnimation}
  on:pointerenter={pointerenter}
  on:pointerleave={pointerleave}
/>
