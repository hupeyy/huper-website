<script>
    import "../app.css";
    import "./global.css";
    import Header from "../lib/components/Header.svelte";
    import Footer from "../lib/components/Footer.svelte";
</script>

<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">

<Header />
<slot />
<Footer />
