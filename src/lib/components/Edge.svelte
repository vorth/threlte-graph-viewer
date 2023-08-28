<script>
  import { T } from '@threlte/core'
  import { Quaternion, Matrix4, Vector3 } from 'three';

  export let p1 = [ 0, 0, 0 ];
  export let p2 = [ 1, 0, 0 ];
  export let radius = 0.1;
  export let color = '#CE00F8';

  $: vector = p2 .map( (x,i) => x - p1[i] );
  $: center = p1 .map( (x,i) => x + 0.5 * vector[ i ] );
  $: length = Math.sqrt( vector .reduce( (sum, x) => sum + x*x, 0 ) );

  const makeRotation = ( from, to ) =>
  {
    if ( !to )
      return new Quaternion();
    const fromV = new Vector3() .fromArray( from ) .normalize();
    const toV = new Vector3() .fromArray( to ) .normalize();
    const axis = new Vector3() .copy( fromV ) .cross( toV ) .normalize();
    if ( axis .equals( new Vector3() ) )
      return new Quaternion();
    const angle = Math.acos( fromV .dot( toV ) );
    const matrix = new Matrix4() .makeRotationAxis( axis, angle );
    return new Quaternion() .setFromRotationMatrix( matrix ) .toArray();
  }

  $: quaternion = makeRotation( [0,1,0], vector );

</script>

<!-- {@debug vector, quaternion} -->

<T.Mesh position={center} {quaternion}>
  <T.CylinderGeometry args={[ radius, radius, length, ]}/>
  <T.MeshStandardMaterial {color} />
</T.Mesh>
