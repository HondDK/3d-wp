<script lang="ts">
  import { T } from '@threlte/core'
  import { PerspectiveCamera } from 'three';
  import { OrbitControls, } from '@threlte/extras';
  import { onMount } from 'svelte';
  export let autoRotate: boolean
  export let enableDamping: boolean
  export let rotateSpeed: number
  export let zoomToCursor: boolean
  export let zoomSpeed: number
  export let minPolarAngle: number
  export let maxPolarAngle: number;
  export let enableZoom: boolean;

  let cameraRef :  PerspectiveCamera;

  let counter = 0;

  const CAMERA_DISTANCE = 150

  // отдаление камеры при onMount
  onMount(() => {
	  const interval = setInterval(() => {
		  if (counter < CAMERA_DISTANCE) {
			  counter += 1;
		  } else {
			  clearInterval(interval);
		  }}, 7); // 1000 ms = 1 second
  });

  $: if (cameraRef) {
		cameraRef.position.set(counter, counter, counter);
  }
</script>

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