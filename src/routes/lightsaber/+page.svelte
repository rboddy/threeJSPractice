<script>
    import { onMount } from "svelte";
    import * as THREE from "three";
    import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

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
        
        const loader = new GLTFLoader();

        loader.load(
            '/QuiGonHilt.glb',

            function(gltf) {
                scene.add(gltf.asset);

                gltf.scene;
                gltf.asset;
            },
            function(xhr) {
                console.log( (xhr.loaded / xhr.total * 100) + '% loaded' );
            },
            function(error) {
                console.error('An error happened')
            }
        )

        camera.position.z = 5;

        function animate() {
            // requestAnimationFrame( animate );
            // saber.rotation.x += 0.005;
            // saber.rotation.y += 0.005;
            renderer.render( scene, camera );
        }
        animate();
        });
</script>

<div id="main"></div>