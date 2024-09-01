<script>
    export let tag = "span";
    export let props = {};
</script>

<svelte:element this={tag} {...props}>
    <slot></slot>
</svelte:element>
