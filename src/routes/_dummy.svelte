<script lang="ts">
  import { browser } from "$app/env";
  import { OutlinePass } from "three/examples/jsm/postprocessing/OutlinePass.js";
  import { Vector2, type Group } from "three";

  import { GLTF, useThrelte, Pass } from "threlte";
  import { useGltfAnimations } from "threlte/extras";

  const { scene, camera } = useThrelte();

  let width = (browser && window.innerWidth) || 1920;
  let height = (browser && window.innerHeight) || 1080;

  const outlinePass = new OutlinePass(
    new Vector2(width, height),
    scene,
    $camera
  );
  outlinePass.edgeStrength = 5;
  outlinePass.enabled = false;

  const { gltf, actions } = useGltfAnimations<"Confused">(({ actions }) => {
    // Either play your animations as soon as they are loaded
    // actions['Take 001']?.play();
    // console.log(actions);
  });

  let dummyModel: Group;
  $: if (dummyModel) {
    outlinePass.selectedObjects = [dummyModel];
  }

  // Or play them whenever you need
  const triggerAnimation = () => {
    $actions["Take 001"]?.play();
    setTimeout(() => {
      $actions["Take 001"]?.stop();
    }, $actions["Take 001"].getClip().duration * 1000);
  };
  const pointerenter = () => {
    document.body.style.cursor = "pointer";
    outlinePass.enabled = true;
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
    outlinePass.enabled = false;
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
  bind:scene={dummyModel}
  bind:gltf={$gltf}
  on:click={triggerAnimation}
  on:pointerenter={pointerenter}
  on:pointerleave={pointerleave}
/>
<Pass pass={outlinePass} />
