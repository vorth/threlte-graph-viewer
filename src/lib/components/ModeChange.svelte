
<script>
  import { T } from '@threlte/core';
  import { interactivity } from '@threlte/extras';

  interactivity();

  export let onChange = () => {};
</script>

<T.Mesh
  position={[-1.4, 1.5, 0.75]}
  on:click={onChange}
  scale={0.3}
  >
  <T.DodecahedronGeometry />
  <T.MeshStandardMaterial color="#F8EBCE" />
</T.Mesh>
