<script>
  import {
    PerspectiveCamera,
    OrbitControls,
    HemisphereLight,
    DirectionalLight,
    Mesh,
    useTexture,
    useThrelte,
  } from "threlte";
  import {
    CircleGeometry,
    MeshBasicMaterial,
    sRGBEncoding,
    EquirectangularReflectionMapping,
  } from "three";
  import { onDestroy } from "svelte";

  const planeMaterial = new MeshBasicMaterial({
    color: 0x000000,
    transparent: true,
    shadowSide: 1,
    opacity: 0.8,
    side: 2,
  });
  const planeGeo = new CircleGeometry(3, 64);

  const { scene } = useThrelte();

  const bgTexture = useTexture("/bg.jpg");
  bgTexture.encoding = sRGBEncoding;
  bgTexture.mapping = EquirectangularReflectionMapping;
  scene.background = bgTexture;

  onDestroy(() => {
    // @ts-ignore
    scene.background.dispose();
  });
</script>

<PerspectiveCamera position={{ x: 0, y: 1, z: 3 }} fov={60}>
  <OrbitControls
    enablePan={true}
    enableRotate
    enableZoom
    enableDamping
    dampingFactor={0.15}
    target={{ x: 0, y: 0, z: 0 }}
  />
</PerspectiveCamera>

<HemisphereLight intensity={0.01} skyColor={0xffffff} />
<DirectionalLight
  intensity={0.4}
  color={0xffffff}
  position={{ x: 1.3, y: 2, z: 4 }}
/>
<Mesh
  material={planeMaterial}
  geometry={planeGeo}
  position={{ x: 0, y: -0.57, z: 0 }}
  rotation={{ x: Math.PI / 2 }}
  receiveShadow
/>
