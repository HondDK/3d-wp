<script lang="ts">
  import { Canvas } from '@threlte/core'
  import Scene from './Scene.svelte'
  import Renderer from '$lib/components/Renderer.svelte';
  import Loader from '$lib/components/Loader.svelte';
  import { Suspense } from '@threlte/extras';
  import Cam from '$lib/components/Cam.svelte';

  let autoRotate: boolean = true
  let enableDamping: boolean = true
  let rotateSpeed: number = 1
  let zoomToCursor: boolean = false
  let zoomSpeed: number = 1
  let minPolarAngle: number = 1
  let maxPolarAngle: number = 1
  let enableZoom: boolean = false

</script>

    <Canvas renderMode={'always'} autoRender={false}>
      <Renderer/>
     <Cam
       {enableDamping}
       {autoRotate}
       {rotateSpeed}
       {zoomToCursor}
       {zoomSpeed}
       {minPolarAngle}
       {maxPolarAngle}
       {enableZoom}
     />
      <Suspense final>
        <Loader slot='fallback'/>
        <Scene/>
      </Suspense>
    </Canvas>







