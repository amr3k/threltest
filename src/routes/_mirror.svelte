<script>
  import { useThrelte } from "threlte";
  import { PlaneBufferGeometry, Color } from "three";
  import { Reflector } from "three/examples/jsm/objects/Reflector";
  import { onDestroy } from "svelte";
  const { scene } = useThrelte();

  const mirrorBack1 = new Reflector(new PlaneBufferGeometry(4, 2), {
    color: new Color(0x7f7f7f),
    textureWidth: window.innerWidth * window.devicePixelRatio,
    textureHeight: window.innerHeight * window.devicePixelRatio,
  });

  mirrorBack1.position.z = -1.5;
  mirrorBack1.position.y = 1;
  scene.add(mirrorBack1);

  onDestroy(() => {
    scene.remove(mirrorBack1);
  });
</script>
