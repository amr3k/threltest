<script lang="ts">
  import {
    PerspectiveCamera,
    OrbitControls,
    HemisphereLight,
    DirectionalLight,
    AmbientLight,
    Mesh,
    useTexture,
    useThrelte,
    useFrame,
    Object3DInstance,
  } from "@threlte/core";
  import {
    Mesh as ThreeMesh,
    CircleGeometry,
    MeshPhongMaterial,
    MeshStandardMaterial,
    sRGBEncoding,
    EquirectangularReflectionMapping,
    WebGLCubeRenderTarget,
    LinearMipmapLinearFilter,
    CubeCamera,
    DoubleSide,
  } from "three";
  import { onDestroy } from "svelte";
  import { cameraIsTweening } from "$lib/store";

  const { scene } = useThrelte();

  const cubeRenderTarget = new WebGLCubeRenderTarget(128, {
    generateMipmaps: true,
    minFilter: LinearMipmapLinearFilter,
    encoding: sRGBEncoding,
  });

  const cubeCamera = new CubeCamera(0.1, 1000, cubeRenderTarget);

  const planeMaterial = new MeshStandardMaterial({
    roughness: 0,
    map: useTexture("/board.jpg"),
    envMap: cubeRenderTarget.texture,
    side: DoubleSide,
  });

  let floorMesh: ThreeMesh;

  useFrame(({ scene: _scene, renderer }) => {
    if (!_scene || !renderer) return;
    floorMesh.visible = false;
    cubeCamera.update(renderer, _scene);
    floorMesh.visible = true;
  });

  const bgTexture = useTexture("/bg.jpg");
  bgTexture.encoding = sRGBEncoding;
  bgTexture.mapping = EquirectangularReflectionMapping;
  scene.background = bgTexture;

  onDestroy(() => {
    planeMaterial.dispose();
    // @ts-ignore
    scene.background.dispose();
    bgTexture.dispose();
  });
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

<Mesh
  bind:mesh={floorMesh}
  material={planeMaterial}
  geometry={new CircleGeometry(3, 64)}
  position={{ x: 0, y: 0, z: 0 }}
  rotation={{ x: Math.PI / -2 }}
  receiveShadow
>
  <!-- <Object3DInstance object={cubeCamera} rotation={{ x: Math.PI / 2 }} /> -->
</Mesh>
