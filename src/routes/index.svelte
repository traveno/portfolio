<script>
import Button from '@smui/button';
import { Canvas } from 'threlte';
import Demo3D from '../components/3d/demo-3d.svelte';
import DemoInteractive from '../components/3d/demo-interactive.svelte';

    /**
    * @type {number | null | undefined}
    */
    let windowHeight;

    /**
    * @type {number | null | undefined}
    */
    let windowWidth;
</script>

<svelte:head>
    <title>Stephen IO</title>
</svelte:head>

<svelte:window bind:innerHeight={windowHeight} bind:innerWidth={windowWidth} />

<h1 class="headline">hi, i'm stephen</h1>



<Demo3D />

<h1 class="headline">i build interactive apps</h1>

<DemoInteractive />


<style>
    .headline {
        font-size: 72px;
        font-family: 'Cascadia Code';
    }

    .headline:after {
        margin-left: 10px;
        content: '';
        width: 30px;
        height: 5px;
        background-color: black;
        opacity: 0;
        display: inline-block;
        animation: blink 1s linear infinite alternate;
    }

    @media (prefers-color-scheme: dark) {
        .headline:after {
            background-color: white;
        }
    }

    @keyframes blink {
        50% {
            opacity: 0;
        }
        100% {
            opacity: 1;
        }
    }
</style>