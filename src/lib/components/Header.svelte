<script>

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

<header class="bg-gray-100 p-4">
    <nav class="flex items-center justify-between max-w-screen-lg mx-auto">
      <a href="/" class="text-2xl font-bold">Alex <br> Huper</a>
      <div class="flex space-x-4">
        <a href="/contact" class="text-base tablet:text-xl">contact</a>
        <a href="/projects" class="text-base tablet:text-xl">projects</a>
        <a href="/resume" class="text-base tablet:text-xl">resume</a>
      </div>
    </nav>
</header>
  