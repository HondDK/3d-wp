<script lang="ts">
  import { Canvas } from '@threlte/core'
  import Scene from './Scene.svelte'
  import Renderer from '$lib/components/Renderer.svelte';
  import { Suspense } from '@threlte/extras';
  import Loader from '$lib/components/Loader.svelte';


  let autoRotate: boolean = true
  let enableDamping: boolean = true
  let rotateSpeed: number = 1
  let zoomToCursor: boolean = false
  let zoomSpeed: number = 1
  let minPolarAngle: number = 0
  let maxPolarAngle: number = Math.PI
  let enableZoom: boolean = true

</script>

    <Canvas autoRender={false}>
      <Renderer/>
      <Suspense>
        <Loader slot='fallback'/>
        <Scene
          {enableDamping}
          {autoRotate}
          {rotateSpeed}
          {zoomToCursor}
          {zoomSpeed}
          {minPolarAngle}
          {maxPolarAngle}
          {enableZoom}
        />
        </Suspense>
    </Canvas>







