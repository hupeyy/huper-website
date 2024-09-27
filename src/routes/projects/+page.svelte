<script>
    import { onMount } from 'svelte';

    let projects = [
        {
            title: 'Blockchain Coin Alert System',
            stack: ['Python', 'Telegram API', 'PostgreSQL'],
            description: 'Developed a blockchain monitoring system with real-time alerts for new coins matching user-tracked keywords. Implemented efficient blockchain data retrieval algorithms and a Telegram bot for user notifications.',
            date: 'Present',
            link: ''
        },
        {
            title: 'ColorStack UF Website',
            stack: ['Svelte', 'Tailwind', 'JavaScript'],
            description: 'Led the development of the About page and collaborated with developers and design teams to implement dynamic components and responsive design with a 95% design-to-development accuracy rate.',
            date: 'August 2024',
            link: 'https://uf.colorstack.org'
        },
        {
            title: 'Genetic Algorithm in Roblox Studio',
            stack: ['Lua'],
            description: 'Developed a genetic algorithm in Roblox Studio, enabling AI to evolve and adapt within the game environment using ray casting for environmental perception.',
            date: 'August 2023',
            link: 'https://github.com/hupeyy/Genetic-Alogrithm---Roblox-Studio'
        },
        {
            title: 'AI-Powered Connect 4 with Minimax',
            stack: ['C++', 'SFML'],
            description: 'Built an AI-driven Connect 4 using Minimax with alpha-beta pruning, improving strategy efficiency by 50%. Designed a user interface to enhance gameplay.',
            date: 'May 2023',
            link: 'https://github.com/hupeyy/Connect_4'
        }
    ];

    let timelineContainer;
    let scrollAmount = 0; // Track the current scroll amount
    let isScrolling = false;
    let timelineWidth = `${projects.length * 90}%`;
    let projectNodes = [];
    let currentProject = 0; // Index of the current project

    onMount(() => {
        const handleWheel = (event) => {
            event.preventDefault();
            scrollAmount += event.deltaY + event.deltaX; // Update the scroll amount based on wheel movement
            if (!isScrolling) {
                smoothScroll(); // Start smooth scrolling if not already started
            }
        };

        const detectMiddleNode = () => {
            const middle = window.innerWidth / 2;

            projectNodes.forEach((node, index) => {
                const rect = node.getBoundingClientRect();
                const nodeMiddle = rect.left + rect.width / 2;

                if (Math.abs(nodeMiddle - middle) < rect.width) {
                    projectNodes.forEach((node) => (node.style.backgroundColor = 'black'));
                    node.style.backgroundColor = '#066375';
                    currentProject = index;
                    const projectContainer = document.querySelector('.project-container');
                    projectContainer.classList.add("animate-slide-in");
                }
            });
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

            detectMiddleNode(); // Make sure to detect the middle node after scrolling.
        };

        timelineContainer.addEventListener('wheel', handleWheel);

        return () => {
            timelineContainer.removeEventListener('wheel', handleWheel);
        };
    });

    // Reactive block to re-render when currentProject changes
    // $: if (currentProject !== undefined) {
    //     // This block will re-run whenever currentProject changes.
    //     console.log('Current project is now:', projects[currentProject].title);
    // }
</script>

<style>
    @tailwind base;
    @tailwind components;
    @tailwind utilities;
    .timeline-container {
        position: relative;
        width: 100%;
        height: 100%;
        overflow-y: hidden; /* Disable vertical scrolling */
        overflow-x: hidden; /* Disable horizontal scrolling but we'll handle it manually */
    }

    .timeline-line {
        position: relative;
        height: 2px;
        width: var(--timeline-width);
        background: black;
    }

    .project-node {
        width: 30px;
        height: 30px;
        border-radius: 50%;
        background: #066375;
        margin: 0 auto; /* Center the node horizontally */
        top: 50%;
        transform: translateY(-50%);
    }

    .project-container {
        @apply fixed max-w-screen-lg w-full transform flex justify-between gap-x-6 p-6
    }

    @keyframes slide-in {
        0% {
            opacity: .5;
            transform: translateY(50%);
        }
        100% {
            opacity: 1;
            transform: translateY(0);
        }
    }

    .animate-slide-in {
        animation: slide-in 0.75s forwards;
    }

    

    
</style>

<title>Projects</title>
<div class=" mx-auto max-w-screen-lg h-[60vh] overflow-hidden">
    <div class="timeline-container" bind:this={timelineContainer} style="--timeline-width: {timelineWidth};">
        <!-- Project container with flexbox layout -->
        <div class="project-container">
            <div class="flex-1">
                <h2 class="text-base tablet:text-lg laptop:text-xl mb-2">{projects[currentProject].title}</h2>
                <div class = "flex flex-wrap gap-x-4 pt-2">
                    {#each projects[currentProject].stack as stackItem, index}
                        <p class="px-2 py-1 rounded-lg bg-gray-400 fill-inherit text-xs font-light tablet:text-sm laptop:text-lg">{projects[currentProject].stack[index] + " "}</p>
                    {/each}
                </div>
                <div class="flex gap-x-4 pt-2">
                    {#if projects[currentProject].link && projects[currentProject].link.includes('github')}
                        <a href="{projects[currentProject].link}" target="_blank">
                            <img src="graphics/github-mark.png" alt="Github logo" class="w-10" />
                        </a>
                    {:else if projects[currentProject].link && projects[currentProject].link.includes('https://')}
                        <a href="{projects[currentProject].link}" target="_blank">
                            <img src="graphics/www-logo.png" alt="Link logo" class="w-10" />
                        </a>
                    {/if}
                </div>
            </div>
            <div class="flex-1">
                <span class="text-xs tablet:text-lg laptop:text-xl">{projects[currentProject].description}</span>
            </div>
        </div>

        <!-- Timeline line with project nodes -->
        <div class="timeline-line mt-[45vh] mx-[50%]">
            {#each projects as project, index}
                <div class="w-40 absolute text-center transform -translate-x-1/2" style="left: {index / (projects.length - 1) * 100}%;">
                    <div class="project-node" bind:this={projectNodes[index]}></div>
                    <p class="laptop:text-lg">{project.date}</p>
                </div>
            {/each}
        </div>
    </div>
</div>
  