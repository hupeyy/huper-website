<script>
    import { onMount } from 'svelte';

    export let leftText = "";
    export let rightText = "";
    export let href = "#"; // Default href, can be overridden

    let gradient = "";
    let currentWidth = 0;

    function generateColorfulGradient(t) {
        const colors = [];

        const width = 100; // Number of steps in the gradient
        for (let x = 0; x <= width; x++) {
            const red = 64 + (128 * x) / width + 64 * Math.sin(t / 2000);
            const green = 64 + (128 * x) / width + 64 * Math.cos(t / 2000);
            const blue = 128;

            colors.push(`rgb(${red}, ${green}, ${blue})`);
        }

        gradient = `linear-gradient(to right, ${colors.join(', ')})`;
    }

    function handleResize() {
        currentWidth = window.innerWidth;
    }


    onMount(() => {
        const updateGradient = (t) => {
            generateColorfulGradient(t);
            requestAnimationFrame(updateGradient);
        };

        requestAnimationFrame(updateGradient);

        window.addEventListener('resize', handleResize);

        return () => {
            window.removeEventListener('resize', handleResize);
        };
    });
</script>

<div id="container" class="connector">
    <span class="text-sm tablet:text-lg">{leftText}</span>
    <div class="gradient-line" style="background-image: {gradient};"></div>
    <a href={href} target="_blank" class="right-text text-sm tablet:text-lg">{rightText}</a>
</div>

<style>
    .connector {
        display: flex;
        align-items: center;
        width: 100%;
        font-family: monospace;
    }

    .gradient-line {
        flex-grow: 1;
        height: 2px;
        margin: 0 10px;
        background-size: 200% 100%;
        animation: moveGradient 6s linear infinite;
    }

    .right-text {
        text-decoration: none;
        color: inherit; /* Inherit color from parent */
    }

    .right-text:hover {
        text-decoration: underline; /* Optional: Add underline on hover */
    }

    @keyframes moveGradient {
        0% {
            background-position: 200% 0;
        }
        100% {
            background-position: -200% 0;
        }
    }
</style>
