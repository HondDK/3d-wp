<script>
  import {Billboard, HTML} from "@threlte/extras";

  export let position = [0, 0, 0]
  export let imageSrc = ''
</script>

<Billboard follow={false} >
  <HTML
    scale={15}
    transform
    {position}
  >
    <img alt='aboba' src={imageSrc} />
  </HTML>
</Billboard>