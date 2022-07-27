<script lang="ts">
  import { Mesh, useFrame, useTexture, useThrelte } from "@threlte/core";
  import type { Mesh as ThreeMesh } from "three";
  import {
    CircleGeometry,
    MeshStandardMaterial,
    sRGBEncoding,
    EquirectangularReflectionMapping,
    WebGLCubeRenderTarget,
    LinearMipmapLinearFilter,
    CubeCamera,
    DoubleSide,
  } from "three";
  import { onDestroy } from "svelte";

  const { scene } = useThrelte();

  const bgTexture = useTexture("/bg.jpg");
  bgTexture.encoding = sRGBEncoding;
  bgTexture.mapping = EquirectangularReflectionMapping;
  scene.background = bgTexture;

  let floorMesh: ThreeMesh;

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
  useFrame(({ scene: _scene, renderer }) => {
    if (!_scene || !renderer) return;
    floorMesh.visible = false;
    cubeCamera.update(renderer, _scene);
    floorMesh.visible = true;
  });

  onDestroy(() => {
    planeMaterial.dispose();
    // @ts-ignore
    scene.background.dispose();
    bgTexture.dispose();
  });
</script>

<Mesh
  bind:mesh={floorMesh}
  material={planeMaterial}
  geometry={new CircleGeometry(3, 64)}
  position={{ x: 0, y: 0, z: 0 }}
  rotation={{ x: Math.PI / -2 }}
  receiveShadow
/>
