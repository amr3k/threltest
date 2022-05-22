<script lang="ts">
  import { GLTF } from "threlte";

  const degreeToRadian = (num: number) => num * (Math.PI / 180);

  const pointerenter = () => {
    document.body.style.cursor = "pointer";
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
  };
</script>

<GLTF
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
