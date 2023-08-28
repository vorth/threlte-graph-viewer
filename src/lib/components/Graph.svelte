<script>
  import { T } from '@threlte/core';
  import Edge from './Edge.svelte';

  export let graph = {
    vertices: [
      [ 0, 0, 1 ],
      [ 0, 1, 0 ],
      [ 1, 0, 0 ],
    ],
    edges: [
      [ 0, 1 ], [ 1, 2 ], [ 2, 0 ], 
    ],
  }

  export let nodeScale = 0.2;
  export let vertexColor = '#00C8AE';
  export let edgeColor = '#F85E00'

</script>


{#each graph.vertices as vertex}
  <T.Mesh
    position={vertex}
    scale={nodeScale}
  >
    <T.SphereGeometry />
    <T.MeshStandardMaterial color={vertexColor} />
  </T.Mesh>
{/each}

{#each graph.edges as [ e1, e2 ]}
  <Edge p1={graph.vertices[ e1 ]} p2={graph.vertices[ e2 ]} radius={nodeScale * 0.4} color={edgeColor}/>
{/each}