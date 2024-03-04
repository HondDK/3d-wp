<script>
  import { HTML } from "@threlte/extras";
  import {onMount} from "svelte";
  export let position = [0, 0, 0];

  export let imageSrc = ''
  let photoRef
  let isLoading = true; // добавляем переменную состояния

  // при onMount ставим обращение фотографий в центр сцены
  onMount(() => {
    photoRef.lookAt(0, 0, 0);
  });
</script>


  <HTML
    on:create={({ ref }) => photoRef = ref}
    scale={15}
    transform
    {position}
  >
    {#if isLoading} <!-- отображаем loader, пока изображение загружается -->
      <div class="loader"></div>
    {/if}
    <img width='250' alt='aboba' src={imageSrc} on:load={() => isLoading = false} /> <!-- когда изображение загружено, устанавливаем isLoading в false -->
  </HTML>

<style>
  img{
          backface-visibility: hidden; /*не работает*/
  }

  .loader {
    border: 16px solid black;
    border-top: 16px solid #1577F5;;
    border-radius: 50%;
    width: 120px;
    height: 120px;
    animation: spin 2s linear infinite;
  }

  @keyframes spin {
    0% { transform: rotate(0deg); }
    100% { transform: rotate(360deg); }
  }
</style>