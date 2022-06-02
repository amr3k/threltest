<script lang="ts">
  import { GLTF } from "threlte";

  const degreeToRadian = (num: number) => num * (Math.PI / 180);
</script>

<GLTF
  url="/duck.glb"
  position={{ x: 0, y: 0, z: 0 }}
  scale={{ x: 0.1, y: 0.1, z: 0.1 }}
  rotation={{
    x: degreeToRadian(90),
    y: degreeToRadian(180),
    z: degreeToRadian(-140),
  }}
  dracoDecoderPath="https://www.gstatic.com/draco/v1/decoders/"
  castShadow
  receiveShadow
  interactive
/>
