<script>
import * as THREE from 'three';
import {
    AmbientLight,
    DirectionalLight,
    OrbitControls,
    PerspectiveCamera,
    OrthographicCamera,
    useThrelte,
    useFrame,
    Mesh,
    Text,
    FogExp2,
} from 'threlte'
import { spring } from 'svelte/motion';
import Keyboard from './keyboard.svelte';
import { onMount } from 'svelte';
import { delay } from './util';

    const { scene } = useThrelte();

    scene.background = new THREE.Color( 0x000000 );
    scene.add(new THREE.GridHelper(100, 50, 0x555555, 0x222222));

    onMount(() => {
    });

    /**
    * @param {any} index
    */
    export function setDemoStage(index) {
        switch (index) {
            case 1:
                spotlightVisibility = true;
                break;
            case 2:
                torusVisibility = true;
                break;
            case 3:
                torusVisibility2 = true;
                break;
            default:
                break;
        }
    }

    

    let spotlightVisibility = false;
    let torusVisibility = false;
    let torusVisibility2 = false;
    let torusRotation = 0;

    const cameraZoom = spring(35);

    useFrame(() => {
        torusRotation += 0.03;
    })

    /**
    * @param {number} zoomLevel
    */
    export function setCameraZoom(zoomLevel) {
        $cameraZoom = zoomLevel;
    }
</script>

<OrthographicCamera position={{ x: 25, y: 25, z: 25 }}  lookAt={{ x: -2, y: 0, z: -5 }} zoom={$cameraZoom} near={5} far={500} >
</OrthographicCamera>

<DirectionalLight shadow position={{ x: 3, y: 5, z: -5 }} target={{ x: 0, y: 0, z: -5 }}/>
<DirectionalLight position={{ x: -3, y: 10, z: -10 }} intensity={0.5} />
<AmbientLight intensity={0.2} />

 <!-- Floor -->
<Mesh
    receiveShadow
    rotation={{ x: -90 * (Math.PI / 180) }}
    geometry={new THREE.CircleBufferGeometry(5, 72)}
    material={new THREE.MeshStandardMaterial({ side: THREE.DoubleSide, color: 0x7a6e00 })}
    position={new THREE.Vector3(0, -0.05, -5)}
    visible={spotlightVisibility}
/>

<Mesh
    geometry={new THREE.TorusGeometry(10, 2, 16, 25)}
    material={new THREE.MeshStandardMaterial({ color: 0x995599 })}
    scale={0.1}
    position={new THREE.Vector3(0, 3, -5)}
    visible={torusVisibility}
    rotation={{ y: torusRotation }}
    castShadow
/>

<Mesh
    geometry={new THREE.TorusGeometry(10, 2, 16, 25)}
    material={new THREE.MeshStandardMaterial({ color: 0x005599 })}
    scale={0.2}
    position={new THREE.Vector3(0, 3, -5)}
    visible={torusVisibility2}
    rotation={{ x: torusRotation }}
    castShadow
/>

<!-- <FogExp2 color={0x000000} density={0.03} /> -->