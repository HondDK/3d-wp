<script>
  import { HTML } from "@threlte/extras";
  import {onMount} from "svelte";
  export let position = [0, 0, 0];

  export let imageSrc = ''
  let photoRef

  // при onMount ставим обращение фотографий в центр сцены
  onMount(() => {
    photoRef.lookAt(0, 0, 0);
  });
</script>
;,

  <HTML
    on:create={({ ref }) => photoRef = ref}
    scale={15}
    transform
    {position}
  >
    <img width='250' alt='aboba' src={imageSrc} /> <!-- когда изображение загружено, устанавливаем isLoading в false -->
  </HTML>

<style>
		img{
						-webkit-transform: rotateX(180deg);
						-webkit-backface-visibility: hidden;
						-webkit-transform: translate3d(0,0,0);

		}

</style>