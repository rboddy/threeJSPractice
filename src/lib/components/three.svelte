<script>
  import { onMount } from "svelte";
  import * as THREE from "three";

  onMount(() => {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    document.getElementById("main").appendChild(renderer.domElement);

    const directionalLight = new THREE.DirectionalLight( 0xffffff, 0.7 );
    scene.add( directionalLight );
    const light = new THREE.PointLight( 0xff0000, 5, 100 );
    light.position.set( 0, 0, 50 );
    scene.add( light );
    const geometry = new THREE.BoxGeometry(2, 2, 2);
    const material = new THREE.MeshLambertMaterial( { color: 0xFFBF00 } )
    const cube = new THREE.Mesh( geometry, material );
    scene.add( cube )

    camera.position.z = 5;

    function animate() {
      requestAnimationFrame( animate );
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
      renderer.render( scene, camera );
    }
    animate();
    });
</script>

<div id="main"></div>
