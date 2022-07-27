<script lang="ts">
  import { HTML } from "@threlte/extras";

  function onClick() {
    console.log("clicked");
  }
</script>

<HTML
  transform
  position={{ x: 1.5, y: 0.01, z: 1.5 }}
  rotation={{ x: Math.PI / -2 }}
  distanceFactor={0.9}
>
  <button on:click={onClick}>Move the camera</button>
</HTML>

<style>
  button {
    background: hsl(253, 97%, 40%);
    border: 1px solid hsl(249, 99%, 47%);
    border-radius: 3px;
    color: rgb(243, 230, 230);
    font-size: 1em;
    padding: 0.5em 1em;
    cursor: pointer;
  }
</style>
