<script>
  import { T } from '@threlte/core'
  import { ContactShadows, Grid, OrbitControls } from '@threlte/extras'
  import { interactivity } from '@threlte/extras'

  import Graph from './Graph.svelte';

  interactivity()

  let smallScale = 0.07;
  let largeScale = 0.14;
  let small = true;
  $: scale = small? smallScale : largeScale;

  const changeScale = () => small = !small;

  const phi = ( 1 + Math.sqrt(5) ) / 2;
  
  const K5 = {
    vertices: [
      [ 1, 1, 1 ],
      [ 1/phi, phi, 0 ],
      [ -1/phi, phi, 0 ],
      [ -1, 1, 1 ],
      [ 0, 1/phi, phi ],
    ],
    edges: [
      [ 0, 1 ], [ 1, 2 ], [ 3, 2 ], [ 3, 4 ], [ 4, 0 ],
      [ 0, 2 ], [ 0, 3 ], [ 1, 3 ], [ 1, 4 ], [ 2, 4 ]
    ],
  }

  let graph=K5;
</script>

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

<T.Mesh
  position={[-1.4, 1.5, 0.75]}
  on:click={changeScale}
  scale={0.3}
>
  <T.DodecahedronGeometry />
  <T.MeshStandardMaterial color="#F8EBCE" />
</T.Mesh>

<Graph nodeScale={scale} {graph} />