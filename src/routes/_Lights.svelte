<script>
  import {
    HemisphereLight,
    DirectionalLight,
    AmbientLight,
  } from "@threlte/core";
</script>

<AmbientLight color={0xffffff} intensity={0.05} />
<HemisphereLight intensity={0.01} skyColor={0xffffff} />

<DirectionalLight
  intensity={1}
  color={0xffffff}
  position={{ x: 1.3, y: 2, z: 4 }}
  target={{ x: 0, y: 0, z: 0 }}
  shadow
/>
<DirectionalLight
  intensity={0.4}
  color={0xffffff}
  position={{ x: -2, y: 1.3, z: 0 }}
  target={{ x: 0, y: 0, z: 0 }}
  shadow
/>
