<script>
    import SpaceFiller from "$lib/components/SpaceFiller.svelte";
    import { onMount } from 'svelte';

    let currScreenWidth;

    const handleResize = () => {
        currScreenWidth = window.innerWidth;
    };

    onMount(() => {
        currScreenWidth = window.innerWidth; // Set initial value when component mounts
        window.addEventListener('resize', handleResize);
        return () => {
            window.removeEventListener('resize', handleResize);
        };
    });
</script>

<div class="mt-8 mx-auto px-10 max-w-screen-lg py-6 ">
    <SpaceFiller
    leftText="Email"
    rightText="alexanderhuper@gmail.com"
    href="mailto:alexanderhuper@gmail.com?subject=Hello From Your Website"
    />    
    <SpaceFiller leftText="GitHub" rightText="hupeyy" href="https://github.com/hupeyy"/>
    <SpaceFiller leftText="LinkedIn" rightText="alexander-huper" href="https://www.linkedin.com/in/alex-huper/" />
</div>
