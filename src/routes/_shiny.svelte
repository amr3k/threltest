<script>
  import { useThrelte } from "threlte";
  import {
    Mesh,
    SphereGeometry,
    MeshPhongMaterial,
    CubeCamera,
    Object3D,
    LinearMipmapLinearFilter,
    WebGLCubeRenderTarget,
  } from "three";
  import { onDestroy } from "svelte";

  const { scene } = useThrelte();

  const cubeRenderTarget = new WebGLCubeRenderTarget(128, {
    generateMipmaps: true,
    minFilter: LinearMipmapLinearFilter,
  });
  const cubeCamera = new CubeCamera(0.1, 1000, cubeRenderTarget);
  const material = new MeshPhongMaterial({
    envMap: cubeRenderTarget.texture,
    reflectivity: 1,
    shininess: 100,
  });
  const pivot = new Object3D();

  const ball = new Mesh(new SphereGeometry(0.5, 32, 32), material);
  ball.position.set(0, 0.5, 1);
  ball.castShadow = true;
  ball.receiveShadow = true;
  ball.add(cubeCamera);
  pivot.add(ball);
  scene.add(pivot);

  onDestroy(() => {
    scene.remove(pivot);
  });
</script>
