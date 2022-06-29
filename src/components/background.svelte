<script>
    import { Canvas } from 'threlte'
    import { onMount } from 'svelte';
    import Scene from './scene.svelte';
    import OverlayScene from './overlay-scene.svelte';
    import { delay } from './util';
    import Snackbar, { Actions, Label } from '@smui/snackbar';
    import Button from '@smui/button';


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
        overlayScene.setCameraZoom(75);
        await overlayScene.say('// hi! welcome to my portfolio!');
        await delay(1000);
        await overlayScene.say('// let\'s have some fun');
        await delay(500);
        overlayScene.setCameraPosition(25, 25, 20);
        overlayScene.setCameraLookAt(-2, 0, -10);
        await overlayScene.say('<MeshSpotLight color={{ 0x7a6e00 }} />')
        await delay(500);
        primaryScene.setDemoStage(1);
        await delay(500);
        primaryScene.setCameraZoom(75);
        await delay(500);
        await overlayScene.say('<MeshTorus rotation={{ x: xRot }} scale={0.1} />');
        await delay(500);
        primaryScene.setDemoStage(2);
        await delay(1000);
        await overlayScene.say('<MeshTorus rotation={{ y: xRot }} scale={0.2} />');
        await delay(500);
        primaryScene.setDemoStage(3);
        await delay(1000);
        await overlayScene.say('// yawn... let\'s kick it up a notch...');
        demoSnackbar.open();
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

<div id="primary-scene">
    <Canvas >
        <Scene bind:this={primaryScene} />
    </Canvas>
</div>

<div id="overlay-scene">
    <Canvas>
        <OverlayScene bind:this={overlayScene} on:loaded={runDemoSequence} />
    </Canvas>
</div> 

<Snackbar variant="stacked" bind:this={demoSnackbar} on:SMUISnackbar:closed={handleClosedSnackbar} timeoutMs={-1}>
    <Label>Continue this demonstration?</Label>
    <Actions>
        <Button>Yes!</Button>
    </Actions>
</Snackbar>

<style>
    #primary-scene {
        position: absolute;
        z-index: -2;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
    }

    #overlay-scene {
        position: absolute;
        z-index: -1;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
    }
</style> 