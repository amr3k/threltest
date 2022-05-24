<script lang="ts">
  import { GLTF, Group, Mesh, Pass, useThrelte } from "threlte";
  import { useGltfAnimations } from "threlte/extras";
  import type { Group as THREEGroup, Object3D, SkinnedMesh, Bone } from "three";
  import { Vector2, BoxBufferGeometry, MeshBasicMaterial } from "three";
  import { browser } from "$app/env";
  import { OutlinePass } from "three/examples/jsm/postprocessing/OutlinePass.js";

  const { scene, camera } = useThrelte();

  let width = (browser && window.innerWidth) || 1920;
  let height = (browser && window.innerHeight) || 1080;

  const outlinePass = new OutlinePass(
    new Vector2(width, height),
    scene,
    $camera
  );
  outlinePass.edgeStrength = 5;
  outlinePass.enabled = false;

  let pathModel: THREEGroup;

  $: if (pathModel) {
    outlinePass.selectedObjects = [pathModel];
    // console.log(
    //   scene.children[0].children[0].children[0].children[0].children[0].children
    // );
    // pathModel.traverse((child) => {
    //   frameObjectArray.push(child);
    //   console.log(child.type);
    // });
  }

  const { gltf, actions } = useGltfAnimations<"Confused">(({ actions }) => {
    // actions['Confused']?.play();
  });

  const triggerAnimation = () => {
    $actions["Confused"]?.play();
    setTimeout(() => {
      $actions["Confused"]?.stop();
    }, $actions["Confused"].getClip().duration * 1000);
    // console.log($actions["Confused"]?.getClip().duration);
  };
  const pointerenter = () => {
    document.body.style.cursor = "pointer";
    outlinePass.enabled = true;
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
    outlinePass.enabled = false;
  };
</script>

<Group
  position={{ x: -1, y: -0.55, z: 0 }}
  rotation={{ y: -90 * (Math.PI / 180) }}
>
  <GLTF
    url={"/pathfinder.glb"}
    dracoDecoderPath="https://www.gstatic.com/draco/v1/decoders/"
    castShadow
    receiveShadow
    bind:gltf={$gltf}
    bind:scene={pathModel}
    on:click={triggerAnimation}
    on:pointerenter={pointerenter}
    on:pointerleave={pointerleave}
  />
  <Mesh
    interactive
    position={{ y: 1 }}
    on:click={triggerAnimation}
    on:pointerenter={pointerenter}
    on:pointerleave={pointerleave}
    geometry={new BoxBufferGeometry(0.6, 2, 0.7)}
    material={new MeshBasicMaterial()}
    visible={false}
  />
</Group>
<!-- {#if frameVisible}
  {#each frameObjectArray as _obj}
    <Mesh
      interactive
      position={{ z: -2 }}
      rotation={{ x: Math.PI / 2, z: Math.PI / -2 }}
      geometry={_obj.geometry}
      material={_obj.material}
      on:click={triggerAnimation}
      on:pointerenter={pointerenter}
      on:pointerleave={pointerleave}
    />
  {/each}
{/if} -->

<Pass pass={outlinePass} />
