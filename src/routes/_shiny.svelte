<script lang="ts">
  import { Mesh, Object3DInstance, useFrame } from "@threlte/core";
  import {
    Mesh as ThreeMesh,
    SphereGeometry,
    MeshPhongMaterial,
    CubeCamera,
    LinearMipmapLinearFilter,
    WebGLCubeRenderTarget,
    sRGBEncoding,
  } from "three";

  const cubeRenderTarget = new WebGLCubeRenderTarget(128, {
    generateMipmaps: true,
    minFilter: LinearMipmapLinearFilter,
    encoding: sRGBEncoding,
  });

  const cubeCamera = new CubeCamera(0.1, 1000, cubeRenderTarget);

  const ballMaterial = new MeshPhongMaterial({
    // color: 0x7f7f7f,
    envMap: cubeRenderTarget.texture,
  });

  let mesh: ThreeMesh;

  useFrame(({ scene, renderer }) => {
    if (!scene || !renderer) return;
    mesh.visible = false;
    cubeCamera.update(renderer, scene);
    mesh.visible = true;
  });
</script>

<Mesh
  bind:mesh
  geometry={new SphereGeometry(0.5, 32, 32)}
  material={ballMaterial}
  castShadow
  receiveShadow
  position={{ y: 0.5, z: 1 }}
>
  <Object3DInstance object={cubeCamera} />
</Mesh>
