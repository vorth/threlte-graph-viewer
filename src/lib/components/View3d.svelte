<script>
  import { Canvas, T } from '@threlte/core'
  import { ContactShadows, Grid, OrbitControls } from '@threlte/extras'
</script>

<Canvas>

  <T.PerspectiveCamera makeDefault position={[2,3,4]} fov={35} >
    <OrbitControls />
  </T.PerspectiveCamera>
  
  <T.DirectionalLight
    intensity={0.8}
    position.x={5}
    position.y={10}
  />
  <T.AmbientLight intensity={0.2} />
  
  <Grid
    position.y={-0.001}
    cellColor="#ffffff"
    sectionColor="#ffffff"
    sectionThickness={1}
    fadeDistance={125}
    cellSize={1}
  />
  
  <ContactShadows
    scale={10}
    blur={2}
    far={2.5}
    opacity={0.5}
  />
  
  <slot/>

</Canvas>
