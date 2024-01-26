<script>
  import View3d from './View3d.svelte'
  import Graph from './Graph.svelte';
	import ModeChange from './ModeChange.svelte';

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

<View3d>

  <ModeChange onChange={changeScale} />

  <Graph nodeScale={scale} {graph} />

</View3d>