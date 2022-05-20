<script>
  import {
    PerspectiveCamera,
    OrbitControls,
    HemisphereLight,
    DirectionalLight,
    Mesh,
  } from "threlte";
  import { CircleGeometry, MeshBasicMaterial } from "three";

  const planeMaterial = new MeshBasicMaterial({
    color: 0xaaaaaa,
    transparent: true,
    shadowSide: 1,
    opacity: 0.8,
    side: 2,
  });
  const planeGeo = new CircleGeometry(3, 64);
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
  intensity={0.1}
  color={0xffffff}
  position={{ x: 1.3, y: 1, z: 4 }}
/>
<Mesh
  material={planeMaterial}
  geometry={planeGeo}
  position={{ x: 0, y: -0.57, z: 0 }}
  rotation={{ x: Math.PI / 2 }}
  receiveShadow
/>
