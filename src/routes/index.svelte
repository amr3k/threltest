<script>
  import { Canvas } from "threlte";
  import Scene from "./_Scene.svelte";
  import Object from "./_Object.svelte";
</script>

<main>
  <Canvas>
    <Scene />
    <Object />
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
