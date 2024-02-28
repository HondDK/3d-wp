<script lang="ts">
  import { T } from '@threlte/core'
  import { OrbitControls, Stars } from '@threlte/extras'
  import Tulips from '$lib/components/models/Tulips.svelte';
  import { onMount } from 'svelte';
  import { PerspectiveCamera } from 'three';

  export let autoRotate: boolean
  export let enableDamping: boolean
  export let rotateSpeed: number
  export let zoomToCursor: boolean
  export let zoomSpeed: number
  export let minPolarAngle: number
  export let maxPolarAngle: number
  export let enableZoom: boolean

  let counter = 0;
  let cameraRef :  PerspectiveCamera ;

  onMount(() => {
    const interval = setInterval(() => {
      if (counter < 250) {
        counter += 1;
      } else {
        clearInterval(interval);
      }}, 7); // 1000 ms = 1 second
  });

  // Reactive statement to update camera position when counter changes
  $: if (cameraRef) {
    cameraRef.position.set(counter, counter, counter);
  }
</script>

<Stars />

<T.PerspectiveCamera
  makeDefault
  position={[0, 1, 1]}
  fov={90}
  on:create={({ ref }) => {
   cameraRef = ref;
  }}
>
  <OrbitControls
    {enableDamping}
    {autoRotate}
    {rotateSpeed}
    {zoomToCursor}
    {zoomSpeed}
    {minPolarAngle}
    {maxPolarAngle}
    {enableZoom}
  />
</T.PerspectiveCamera>

<Tulips/>
