<script lang="ts">
  import { GLTF } from "threlte";
  import { useGltfAnimations } from "threlte/extras";

  const { gltf, actions } = useGltfAnimations<"Confused">(({ actions }) => {
    // Either play your animations as soon as they are loaded
    actions["Take 001"]?.play();
  });
</script>

<GLTF
  url={"/girl.glb"}
  position={{ x: -1, y: 0.57, z: 0 }}
  scale={{ x: 0.003, y: 0.003, z: 0.003 }}
  dracoDecoderPath="https://www.gstatic.com/draco/v1/decoders/"
  castShadow
  receiveShadow
  interactive
  bind:gltf={$gltf}
/>
