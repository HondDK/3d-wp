<script lang="ts">
  import {HTML, useSuspense} from "@threlte/extras";
  import {onMount} from "svelte";
  import { blur } from 'svelte/transition';
  export let position = [0, 0, 0];

  let loaded = false;

  function handleLoad() {
    loaded = true;
  }

  export let imageSrc = ''
  const suspend = useSuspense();
  let photoRef

  // при onMount ставим обращение фотографий в центр сцены
  onMount(() => {
    photoRef.lookAt(0, 0, 0);
    suspend(promiseImageLoad(imageSrc));
  });

  function promiseImageLoad(imageSrc) {
    return new Promise((resolve, reject) => {
      const img = new Image();
      img.onload = () => resolve(img);
      img.onerror = reject;
      img.src = imageSrc;
    });
  }
</script>

    <HTML
      pointerEvents={'inherit'}
      sprite
      on:create={({ ref }) => photoRef = ref}
      scale={15}
      transform
      {position}
    >
    <img width='250' alt='aboba' src={imageSrc} in:blur={{ duration: loaded ? 1000 : 0 }} on:load={handleLoad} />
    </HTML>

<style>
   img{

   }
</style>
```