<script>
    import { Canvas } from 'threlte'
    import { onMount } from 'svelte';
    import Scene from './scene.svelte';
    import OverlayScene from './overlay-scene.svelte';
    import { delay } from '../util';

    /**
    * @type {number}
    */
    let containerWidth;

    /**
    * @type {number}
    */
    let containerHeight;


    /**
    * @type {any}
    */
    let demoSnackbar;

    /**
    * @type {Scene}
    */
    let primaryScene;

    /**
     * @type {OverlayScene}
     */
    let overlayScene;

    onMount(() => {
    });

    async function runDemoSequence() {
        overlayScene.setCameraPosition(25, 25, 27);
        overlayScene.setCameraLookAt(-2, 0, -3);
        overlayScene.setCameraZoom(50);
        await overlayScene.say('// welcome to my portfolio!');
        await delay(1000);
        await overlayScene.say('// let\'s have some fun');
        await delay(500);
        overlayScene.setCameraPosition(25, 25, 20);
        overlayScene.setCameraLookAt(-2, 0, -10);
        await overlayScene.say('<MeshSpotLight color={{ 0x7a6e00 }} />')
        await delay(500);
        primaryScene.setDemoStage(1);
        await delay(500);
        primaryScene.setCameraZoom(50);
        await delay(500);
        await overlayScene.say('<MeshTorus rotation={{ x: xRot }} scale={0.1} />');
        await delay(500);
        primaryScene.setDemoStage(2);
        await delay(1000);
        await overlayScene.say('<MeshTorus rotation={{ y: xRot }} scale={0.2} />');
        await delay(500);
        primaryScene.setDemoStage(3);
        await delay(1000);
        //demoSnackbar.open();
        runFullSequence();
    }

    async function runFullSequence() {
        await overlayScene.say('// great! let\'s keep going');
        await delay(1000);
        await overlayScene.say('// check this out');
        await delay(500);
        primaryScene.setDemoStage(4);
        await delay(500);
        primaryScene.setDemoStage(5);
        await delay(5000);
        await overlayScene.say('// let\'s get rid of this grid');
        await delay(500);
        await overlayScene.say('scene.remove(grid);');
        await delay(500);
        primaryScene.setDemoStage(6);
        await delay(3000);
        await overlayScene.say('// much better');
        await delay(1000);
        await overlayScene.say('// ok... let\'s keep moving');
        await delay(500);
        await overlayScene.say('// another trick for you');
        await delay(1000);
        primaryScene.setDemoStage(7);
        await delay(6000);
        primaryScene.setDemoStage(8);
    }

    /**
    * @param {any} event
    */
    function handleClosedSnackbar(event) {
        runFullSequence();
    }
</script>

<div class="demo-container" bind:clientWidth={containerWidth} bind:clientHeight={containerHeight}>
    <div id="primary-scene">
        <Canvas size={{ width: containerWidth, height: containerWidth * 0.5 }}>
            <Scene bind:this={primaryScene} />
        </Canvas>
    </div>
    <div id="overlay-scene">
        <Canvas size={{ width: containerWidth, height: containerWidth * 0.5 }}>
            <OverlayScene bind:this={overlayScene} on:loaded={runDemoSequence} />
        </Canvas>
    </div>
</div>



<style>
    .demo-container {
        width: 100%;
        display: grid;
        border-radius: 50px;
        overflow: hidden;
    }


    #primary-scene {
        grid-area: 1 / 1;
    }

    #overlay-scene {
        grid-area: 1 / 1;
    }
</style> 