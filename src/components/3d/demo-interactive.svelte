<script>
import { onMount } from 'svelte';

import { Canvas } from 'threlte';
import Scene from './demo-interactive-scene.svelte';
import Slider from '@smui/slider';

    /**
    * @type {number}
    */
    let containerHeight;

    /**
    * @type {number}
    */
    let containerWidth;

    onMount(() => {
        console.log(containerWidth, containerHeight);
    })

    let animSpeed = 0.5;
    let cameraZoom = 0;
    let cylinderLength = 0.01;
</script>

<div id="demo-interactive" bind:clientWidth={containerWidth} bind:clientHeight={containerHeight}>
    <div id="demo-display">
        <Canvas size={{ width: containerWidth * 0.7, height: containerWidth * 0.5 }}>
            <Scene animationSpeed={animSpeed} cameraZoom={cameraZoom} cylinderLength={cylinderLength} />
        </Canvas>
    </div>
    <div id="demo-controls" width={ containerWidth * 0.3 }>
        <div style="padding: 15px;">
            <h2>ANIMATION SPEED</h2>
            <Slider bind:value={animSpeed} min={0} max={1} step={0.001} />

            <h2>CAMERA ZOOM</h2>
            <Slider bind:value={cameraZoom} min={0} max={1} step={0.001} />

            <h2>CYLINDER LENGTH</h2>
            <Slider bind:value={cylinderLength} min={0.01} max={1} step={0.001} />
        </div>
        
    </div>
</div>

<style>
    #demo-interactive {
        width: 100%;
        max-width: 1200px;
        border-radius: 50px;
        overflow: hidden;

        background-color: rgb(28, 28, 28);
    }

    #demo-controls {
        float: right;
        width: 30%;
        text-align: center;
        font-family: 'Cascadia Code';
        color: darkgray;
    }

    #demo-display {
        width: 70%;
        float: left;
    }
</style>