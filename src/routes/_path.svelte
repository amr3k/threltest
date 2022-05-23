<script lang="ts">
  import { GLTF, Group, Mesh } from "threlte";
  import { useGltfAnimations } from "$lib/threlte/useGltfAnimations";
  import type { Group as THREEGroup, Object3D, SkinnedMesh, Bone } from "three";

  let frameVisible = false;
  let frameObjectArray: (THREEGroup | Object3D | SkinnedMesh | Bone)[] = [];

  let scene: THREEGroup;

  $: if (scene) {
    // console.log(
    //   scene.children[0].children[0].children[0].children[0].children[0].children
    // );
    scene.traverse((child) => {
      frameObjectArray.push(child);
      console.log(child.type);
    });
    frameVisible = true;
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
  };
  const pointerleave = () => {
    document.body.style.cursor = "auto";
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
    bind:scene
  />
  {#if frameVisible}
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
  {/if}
</Group>
