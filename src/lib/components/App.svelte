<script lang="ts">
  import { Canvas } from '@threlte/core'
  import Scene from './Scene.svelte'
  import Renderer from '$lib/components/Renderer.svelte';
  import Loader from '$lib/components/Loader.svelte';
  import { Suspense, Text } from '@threlte/extras';
  import Cam from '$lib/components/Cam.svelte';

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
        <Text
          position.z={-8}
          slot="fallback"
          text="Loading"
          fontSize={1}
          color="white"
          anchorX="50%"
          anchorY="50%"
          on:create={({ ref }) => {
      ref.lookAt(-40, 25, 40)
    }}
        />
        <Scene/>
      </Suspense>
    </Canvas>







