<script lang="ts">
  import { GLTF, useThrelte, Pass } from "threlte";

  import { OutlinePass } from "three/examples/jsm/postprocessing/OutlinePass.js";
  import { Vector2 } from "three";
  import { browser } from "$app/env";
  import type { Group } from "three";

  const degreeToRadian = (num: number) => num * (Math.PI / 180);

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

  let duckModel: Group;

  $: if (duckModel) {
    outlinePass.selectedObjects = [duckModel];
  }
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
  bind:scene={duckModel}
  url="/duck.glb"
  position={{ x: 0, y: -0.57, z: 0 }}
  scale={{ x: 0.3, y: 0.3, z: 0.3 }}
  rotation={{
    x: degreeToRadian(90),
    y: degreeToRadian(180),
    z: degreeToRadian(-140),
  }}
  dracoDecoderPath="https://www.gstatic.com/draco/v1/decoders/"
  castShadow
  receiveShadow
  interactive
  on:click={() => console.log("quack")}
  on:pointerenter={pointerenter}
  on:pointerleave={pointerleave}
/>

<Pass pass={outlinePass} />
