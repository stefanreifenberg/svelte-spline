<script>
import * as THREE from 'three';
import * as SC from "svelte-cubed";
import SplineLoader from '@splinetool/loader';
import { onMount } from "svelte";

let model;

// import spline scene
const loader = new SplineLoader();

onMount(() => {
  loader.load(
  'https://prod.spline.design/6ZQA4GzzFjXNeDE4/scene.splinecode',
  (splineScene) => {
    model = splineScene;
    
  });
});

let spin = 0;

SC.onFrame(() => {
  spin += 0.001;
});
</script>

<SC.Canvas
        antialias
        background={new THREE.Color('#4724c6')}
        shadows={THREE.PCFShadowMap}
>
  
  <SC.Primitive
    object={model}
    scale={[1, 1, 1]}
    position={[0, 0, 0]}
    rotation={[0, spin, 0]}
  />
	
  <SC.PerspectiveCamera position={[1000,10,20]}/>
  <SC.HemisphereLight intensity={0.75} color="#eaeaea" />
  <SC.OrbitControls />
</SC.Canvas>