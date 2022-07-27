<script>
  import { Canvas } from "@threlte/core";
  import Camera from "./_Camera.svelte";
  import Duck from "./_duck.svelte";
  import Buttons from "./_Buttons.svelte";
  import Lights from "./_Lights.svelte";
  import Background from "./_Background.svelte";
</script>

<main>
  <Canvas linear>
    <Camera />
    <Lights />
    <Background />
    <Duck />
    <Buttons />
  </Canvas>
</main>

<style>
  main {
    position: fixed;
    top: 0;
    left: 0;
    width: 100vw;
    height: 100vh;
  }
</style>
