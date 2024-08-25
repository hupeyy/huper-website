<script>
    import { onMount } from 'svelte';

    export let text = [];

    let currentText = '';
    let currentTextIndex = 0;
    let currentCharIndex = 0;
    let typingSpeed = 100;
    let delay = 2000;

    function typeText() {
        if (currentCharIndex < text[currentTextIndex].length) {
            currentText += text[currentTextIndex].charAt(currentCharIndex);
            currentCharIndex++;
            setTimeout(typeText, typingSpeed);
        } else {
            setTimeout(eraseText, delay);
        }
    }

    function eraseText() {
        if (currentCharIndex >= 0) {
            currentText = text[currentTextIndex].substring(0, currentCharIndex);
            currentCharIndex--;
            setTimeout(eraseText, typingSpeed);
        } else {
            currentTextIndex++;
            if (currentTextIndex >= text.length) {
                currentTextIndex = 0;
            }
            setTimeout(typeText, typingSpeed);
        }
    }

    onMount(() => {
        typeText();
    });
</script>

<div class="text-xl font-bold min-h-8">
    {currentText}
</div>