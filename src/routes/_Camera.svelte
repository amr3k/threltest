<script lang="ts">
  import { PerspectiveCamera, OrbitControls } from "@threlte/core";
  import { cameraIsTweening } from "$lib/store";
</script>

<PerspectiveCamera position={{ x: 0, y: 1, z: 3 }} fov={60}>
  {#if !$cameraIsTweening}
    <OrbitControls
      enablePan={true}
      enableRotate
      enableZoom
      enableDamping
      dampingFactor={0.15}
      target={{ x: 0, y: 0, z: 0 }}
    />
  {/if}
</PerspectiveCamera>
