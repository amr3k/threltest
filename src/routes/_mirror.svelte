<script>
  import { onDestroy } from "svelte";
  import { PlaneBufferGeometry, Color } from "three";
  import { Reflector } from "three/examples/jsm/objects/Reflector";
  import { useThrelte } from "@threlte/core";

  const { scene } = useThrelte();

  const mirror = new Reflector(new PlaneBufferGeometry(4, 2), {
    color: new Color(0x7f7f7f),
    textureWidth: window.innerWidth * window.devicePixelRatio,
    textureHeight: window.innerHeight * window.devicePixelRatio,
  });

  mirror.position.z = -1.5;
  mirror.position.y = 1;
  scene.add(mirror);

  onDestroy(() => {
    scene.remove(mirror);
  });
</script>
