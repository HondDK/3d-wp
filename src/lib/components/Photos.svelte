<script>
  import {Billboard, HTML} from "@threlte/extras";
  import {onMount} from "svelte";
  export let position = [0, 0, 0];
  export let imageSrc = '';

  let photoRef

  onMount(() => {
    photoRef.lookAt(0, 0, 0);
  });
</script>

<Billboard
  follow={false}
  lockY
  lockX
  lockZ
>
  <HTML
    on:create={({ ref }) => photoRef = ref}
    scale={15}
    transform
    {position}
  >
    <img alt='aboba' src={imageSrc} />
  </HTML>
</Billboard>