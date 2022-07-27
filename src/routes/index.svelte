<script>
  import { Canvas } from "@threlte/core";
  import Scene from "./_Scene.svelte";
  import Path from "./_path.svelte";
  import Dummy from "./_dummy.svelte";
  import Duck from "./_duck.svelte";
  import Mirror from "./_mirror.svelte";
  import Shiny from "./_shiny.svelte";
  import Buttons from "./_Buttons.svelte";
</script>

<main>
  <Canvas linear>
    <Scene />
    <!-- <Path /> -->
    <Dummy />
    <!-- <Duck /> -->
    <!-- <Mirror /> -->
    <!-- <Shiny /> -->
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
