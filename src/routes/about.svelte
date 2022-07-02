

<h1 class="headline">what keeps me going?</h1>
<p>I create beautiful web-based applications using modern technologies.</p>
<p>Interactive 3D experiences are my spectialty.</p>

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