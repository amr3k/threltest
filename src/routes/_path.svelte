<script lang="ts">
  import { GLTF } from "threlte";
  import { useGltfAnimations } from "$lib/threlte/useGltfAnimations";

  const { gltf, actions } = useGltfAnimations<"Confused">(({ actions }) => {
    // Either play your animations as soon as they are loaded
    // actions['Confused']?.play();
    // console.log(actions['Confused']);
  });

  // Or play them whenever you need
  const triggerAnimation = () => {
    $actions["Confused"]?.play();
    // animations.Confused.play();
  };
  const pointerenter = () => {
    document.body.style.cursor = "pointer";
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
  };
</script>

<GLTF
  url={"/pathfinder.glb"}
  position={{ x: -2, y: -0.55, z: 0 }}
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
