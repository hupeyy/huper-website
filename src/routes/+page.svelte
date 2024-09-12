<script>
    import { onMount } from 'svelte';
    import TypingCarousel from '../lib/components/TypingCarousel.svelte';

    let text = [
        "student",
        "developer",
        "sudoku solver",
    ];
</script>

<title>Alex Huper's Website</title>
<div class="mt-8 mx-auto px-10 max-w-screen-lg">
    <TypingCarousel text={text} />
    <p class="mt-4"> I am a student at the University of Florida studying computer science. </p>
    <img src="graphics/uf.png" alt="University of Florida" class="mt-4 rounded-lg bg-gray" />
</div>