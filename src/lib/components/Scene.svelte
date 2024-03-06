<script lang="ts">
	import { Billboard, Stars, Text } from '@threlte/extras';
  import Tulips from '$lib/components/models/Tulips.svelte';
  import Photos from '$lib/components/Photos.svelte';
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';

  const PHOTO_RADIUS = 300

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
            './images/15.jpeg',
            './images/16.jpeg',
            './images/17.jpeg',
            './images/18.jpeg',
            './images/19.jpeg',
            './images/21.jpeg',
            './images/20.jpeg',
            './images/21.jpeg',
            './images/22.jpeg',
  ]

  // позиции для фотографий
  $: positions = photos.map((_, index, array) => {
    const angle = (index / array.length) * 2 * Math.PI;
    const yPosition = 12
    return [PHOTO_RADIUS * Math.cos(angle), yPosition, PHOTO_RADIUS * Math.sin(angle)];
  });

  let loaded = false;

  onMount(async () => {
    await Promise.all(photos.map(photo => promiseImageLoad(photo)));
    loaded = true;
  });

  function promiseImageLoad(imageSrc) {
    return new Promise((resolve, reject) => {
    const img = new Image();
      img.onload = () => resolve(img);
      img.onerror = reject;
      img.src = imageSrc;
    })}

</script>

<Billboard transition={fade} lockZ>
  <Text font='font/foglihtenno06.ttf' transition={fade} color='#FFDFDF' position={[-145, 280, 0]} scale={200} text='С праздником, дорогие дамы!'/>
</Billboard>

<Stars/>
<Tulips/>

{#if loaded}
  {#each photos as photo, index (photo + Math.random())}
    <Photos position={positions[index]} imageSrc={photo}/>
  {/each}
{/if}

