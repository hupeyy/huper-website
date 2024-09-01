<script>
    import { onMount } from 'svelte';

    let timelineContainer;
    let scrollAmount = 0; // Track the current scroll amount
    let isScrolling = false; // Flag to track if the smooth scrolling is active

    onMount(() => {
        const handleWheel = (event) => {
            event.preventDefault();
            scrollAmount += event.deltaY; // Update the scroll amount based on wheel movement
            if (!isScrolling) {
                smoothScroll(); // Start smooth scrolling if not already started
            }
        };

        const smoothScroll = () => {
            isScrolling = true;
            const currentScroll = timelineContainer.scrollLeft;
            const targetScroll = currentScroll + scrollAmount;

            // Calculate the amount to scroll in each frame for smooth effect
            const scrollStep = (targetScroll - currentScroll) * 0.1;

            if (Math.abs(scrollStep) > 0.5) {
                timelineContainer.scrollLeft += scrollStep;
                scrollAmount -= scrollStep;
                requestAnimationFrame(smoothScroll);
            } else {
                isScrolling = false;
                scrollAmount = 0;
            }
        };

        timelineContainer.addEventListener('wheel', handleWheel);

        return () => {
            timelineContainer.removeEventListener('wheel', handleWheel);
        };
    });
</script>

<style>
    .timeline-container {
        position: relative;
        width: 100%;
        height: 100%; /* Make sure this fills the height of the viewport */
        overflow-y: hidden; /* Disable vertical scrolling */
        overflow-x: hidden; /* Disable horizontal scrolling but we'll handle it manually */
    }

    .timeline-line {
        position: relative;
        height: 2px;
        width: 200vh; /* Extend the width beyond the viewport to allow scrolling */
        background-color: #000000; /* Solid line or dashed as per preference */
        margin: 55% 50%; /* Center the line horizontally */
    }

    .project-node {
        position: absolute;
        width: 30px;
        height: 30px;
        background-color: #000000;
        border-radius: 50%;
        top: 50%; /* Center the nodes on the line vertically */
        transform: translateY(-50%);
    }
</style>

<div class="mt-8 mx-auto px-10 max-w-screen-lg h-[70vh] overflow-hidden">
    <div class="timeline-container" bind:this={timelineContainer}>
        <div class="timeline-line">
            <div class="project-node" style="left: 0%;"></div>
            <div class="project-node" style="left: 25%;"></div>
            <div class="project-node" style="left: 50%;"></div>
            <div class="project-node" style="left: 75%;"></div>
            <div class="project-node" style="left: 100%;"></div>
        </div>
    </div>
</div>
