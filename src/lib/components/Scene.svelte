<script lang="ts">
  import { T } from '@threlte/core'
  import { OrbitControls, Stars } from '@threlte/extras';
  import Tulips from '$lib/components/models/Tulips.svelte';
  import { onMount } from 'svelte';
  import { PerspectiveCamera } from 'three';
  import Photos from '$lib/components/Photos.svelte';

  export let autoRotate: boolean
  export let enableDamping: boolean
  export let rotateSpeed: number
  export let zoomToCursor: boolean
  export let zoomSpeed: number
  export let minPolarAngle: number
  export let maxPolarAngle: number
  export let enableZoom: boolean

  const PHOTO_RADIUS = 260
  const CAMERA_DISTANCE = 160

  const photos = [
		'./images/1.jpeg',
            './images/2.jpeg',
            './images/3.jpeg',
            './images/4.jpeg',
            './images/5.jpeg',
            './images/6.jpeg',
            './images/7.jpeg',
            './images/8.jpeg',
            './images/9.jpeg',
            './images/10.jpeg',
            './images/11.jpeg',
            './images/12.jpeg',
            './images/13.jpeg',
            './images/14.jpeg',
            './images/14.jpeg',
            './images/15.jpeg',
            './images/16.jpeg',
            './images/17.jpeg',
            './images/18.jpeg',
            './images/19.jpeg',
            './images/20.jpeg',
            './images/22.jpeg',
            './images/21.jpeg',
            './images/22.jpeg',
            './images/23.jpeg',
  ]

  let counter = 0;
  let cameraRef :  PerspectiveCamera;

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


  // позиции для фотографий

  $: positions = photos.map((_, index, array) => {
    const angle = (index / array.length) * 2 * Math.PI;
    const yPosition = PHOTO_RADIUS * Math.sin(angle);
    return [PHOTO_RADIUS * Math.cos(angle), yPosition, PHOTO_RADIUS * Math.sin(angle)];
  });
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

{#each photos as photo, index (photo + Math.random())}
  <Photos position={positions[index]} imageSrc={photo}/>
{/each}

<Tulips/>
