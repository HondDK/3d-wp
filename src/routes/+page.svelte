<script lang="ts">
  import App from '$lib/components/App.svelte'
  import Analytics from '$lib/Analytics.svelte';
</script>

<div>
  <App/>
  <Analytics />
</div>

<style>
  :global(body) {
    margin: 0;
  }

  div {
    width: 100dvw;
    height: 100dvh;
    background: rgb(13, 19, 32);
  }
</style>
