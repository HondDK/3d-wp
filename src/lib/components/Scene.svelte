<script lang="ts">
	import { Stars, useSuspense } from '@threlte/extras';
  import Tulips from '$lib/components/models/Tulips.svelte';
  import Photos from '$lib/components/Photos.svelte';
  import { onMount } from 'svelte';

  const PHOTO_RADIUS = 400

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

  let tulipsLoaded = false;

  // позиции для фотографий
  $: positions = photos.map((_, index, array) => {
    const angle = (index / array.length) * 2 * Math.PI;
    const yPosition = 12
    return [PHOTO_RADIUS * Math.cos(angle), yPosition, PHOTO_RADIUS * Math.sin(angle)];
  });

  const { suspended } = useSuspense()
</script>

<Stars />
<Tulips on:loaded={() => tulipsLoaded = true}/>

{#if suspended}
  {#each photos as photo, index (photo + Math.random())}
    <Photos position={positions[index]} imageSrc={photo}/>
  {/each}
{/if}

```
