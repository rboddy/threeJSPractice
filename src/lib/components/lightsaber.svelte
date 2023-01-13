<script>
    import { onMount } from "svelte";
    import * as THREE from "three";
    import { GLTFLoader } from "three/examples/jsm/loaders/GLTFLoader";
  
    onMount(() => {
        // renderer                                                                 
        const renderer = new THREE.WebGLRenderer({antialias: true});
        renderer.setSize(window.innerWidth, window.innerHeight);
        document.body.appendChild(renderer.domElement);

        // camera                                                                   
        const camera = new THREE.PerspectiveCamera(
        40,
        window.innerWidth / window.innerHeight,
        0.01,
        1000
        );

        // scene and lights                                                         
        const scene = new THREE.Scene();
        scene.background = new THREE.Color('grey');
        const light = new THREE.PointLight( 16777215, 100, 0 );
        light.position.set( 30, 10, 0 );
        scene.add( light );

        // load gltf model and texture                            
        const objs = [];
        const loader = new GLTFLoader();
        loader.load("./QuiGonHilt.glb", gltf => {
            const mixer = new THREE.AnimationMixer(gltf.scene);
            // animations is a list of THREE.AnimationClip
            for (const anim of gltf.animations) {
                mixer.clipAction(anim).play();
            }
            gltf.scene.position.set(0, 10, 0);
            gltf.scene.rotation.y += -1;
            
            scene.add(gltf.scene);
            objs.push({gltf, mixer});
        });

        camera.position.set(106, 36, 20); // settings in `sceneList` "Monster"
        camera.up.set(0, 1, 0);
        camera.lookAt(new THREE.Vector3(1, 1, 1));

        (function animate() {
            renderer.render(scene, camera);
            requestAnimationFrame(animate);
        })();
    });
  </script>
  
  <div id="main"></div>