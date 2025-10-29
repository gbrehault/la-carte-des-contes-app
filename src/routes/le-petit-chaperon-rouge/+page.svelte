<script lang="ts">
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import { browser } from "$app/environment";
  import { Volume2, VolumeX } from "lucide-svelte";

  let section: HTMLElement | null = null;
  let video: HTMLVideoElement | null = null;
  let audio: HTMLAudioElement | null = null;
  let isPlaying = false;

  function toggleAudio() {
    if (!audio) return;

    if (isPlaying) {
      audio.pause();
    } else {
      audio.play();
    }

    isPlaying = !isPlaying;
  }

  onMount(() => {
    if (!browser) return; // sécurité SSR

    gsap.registerPlugin(ScrollTrigger);

    if (!section || !video) return;

    const init = () => {
      const dur = video!.duration;
      if (!dur || !isFinite(dur)) return;

      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: section!,
          start: "top top",
          end: () => "+=" + (section!.scrollHeight - window.innerHeight),
          scrub: true,
          invalidateOnRefresh: true,
          // markers: true,
        },
      });

      const st = tl.scrollTrigger!;

      // 🎥 Lecture de la vidéo en fonction du scroll
      tl.to(
        {},
        {
          duration: 1, // adapte selon ton scroll total
          ease: "none",
          onUpdate: () => {
            const p = st.progress; // 0..1
            video!.currentTime = p * dur;
          },
        },
        0
      );

      // (Optionnel) Action à la fin : tu peux ajouter du texte, un fondu, etc.
      tl.call(
        () => {
          console.log("Vidéo terminée !");
        },
        [],
        1
      );

      requestAnimationFrame(() => ScrollTrigger.refresh());
    };

    if (video!.readyState >= 1) init();
    else video!.addEventListener("loadedmetadata", init, { once: true });
  });
</script>

<!-- Section STICKY contenant la vidéo -->
<section bind:this={section} class="relative h-[300vh] bg-gray-100">
  <div
    id="bloc-video"
    class="sticky top-0 h-screen flex items-center justify-center"
  >
    <video
      bind:this={video}
      src="/video/OUTPUT.mp4"
      muted
      playsinline
      preload="auto"
      class="w-full h-full object-cover"
    ></video>
    <!-- Audio caché -->
    <audio bind:this={audio} src="/sound/son.2.mp3" loop></audio>

    <!-- Bouton -->
    <button
      on:click={toggleAudio}
      class="px-5 py-3 fixed bottom-0 right-0 rounded-xl bg-amber-400 m-6 text-white z-50 hover:bg-amber-500 transition"
    >
      {#if isPlaying}
        <Volume2></Volume2>
      {:else}
        <VolumeX></VolumeX>
      {/if}
    </button>
  </div>

  <div>
    <h1 class="text-center font-bold font-title text-5xl relative z-999">
      TEST TEST TEST TEST
    </h1>
  </div>
</section>
