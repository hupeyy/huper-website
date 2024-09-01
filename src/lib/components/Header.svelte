<script>
    export let title = "Alex Huper's Website";

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

<title>{title}</title>
<header class="bg-gray-100 p-4">
    <nav class="flex items-center justify-between max-w-screen-lg mx-auto">
      <a href="/" class="text-2xl font-bold">Alex <br> Huper</a>
      <div class="flex space-x-4">
        <a href="/contact" class="text-lg">contact</a>
        <a href="/projects" class="text-lg">projects</a>
        <a href="/resume" class="text-lg">resume</a>
      </div>
    </nav>
</header>
  