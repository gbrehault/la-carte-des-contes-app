<script lang="ts">
  import favicon from "$lib/assets/favicon.svg";
  import "../app.css";
  let { children } = $props();
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
  <link rel="stylesheet" href="/fonts/font.css" />
</svelte:head>

{@render children?.()}
