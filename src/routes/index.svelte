<script>
  import { Canvas } from "threlte";
  import Scene from "./_Scene.svelte";
  import Path from "./_path.svelte";
  import Dummy from "./_dummy.svelte";
</script>

<main>
  <Canvas>
    <Scene />
    <Path />
    <Dummy />
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
