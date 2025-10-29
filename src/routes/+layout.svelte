<script lang="ts">
  import favicon from "$lib/assets/favicon.svg";
  import { onMount } from "svelte";
  import { afterNavigate } from "$app/navigation";
  import "../app.css";
  let { children } = $props();

  let removed = false;

  function removeSplashScreen() {
    if (removed) return;
    const splash = document.getElementById("app-loader");
    if (splash) {
      splash.style.transition = "opacity 0.2s ease";
      splash.style.opacity = "0";
      setTimeout(() => {
        splash.remove();
      }, 2000);
      removed = true;
    }
  }

  onMount(() => {
    // Laisse le splash visible pendant 2 secondes avant de lancer la disparition
    setTimeout(() => {
      requestAnimationFrame(() => removeSplashScreen());
    }, 2000);

    // Ceinture+bretelles : si une navigation auto arrive, retire aussi après 2s
    afterNavigate(() => {
      setTimeout(() => removeSplashScreen(), 2000);
    });
  });
</script>

<svelte:head>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" />
  <link
    href="https://fonts.googleapis.com/css2?family=Almendra:wght@400;700&family=Aleo:wght@300;400;700&display=swap"
    rel="stylesheet"
  />
  <link rel="icon" href={favicon} />
  <link rel="stylesheet" href="/fonts/font.css" />
  <title>La carte des contes</title>
</svelte:head>
<!-- <Header /> -->

{@render children?.()}
