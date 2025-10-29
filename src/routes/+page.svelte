<script lang="ts">
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";

  gsap.registerPlugin(ScrollTrigger);

  let section: HTMLElement | null = null;
  let video: HTMLVideoElement | null = null;

  onMount(() => {
    const bloc = document.getElementById("bloc-video") as HTMLElement | null;
    if (!bloc || !section || !video) return;

    // État initial : léger zoom + coins arrondis (seront animés)
    gsap.set(bloc, {
      scale: 1,
      transformOrigin: "center center",
    });

    const init = () => {
      const dur = video!.duration;
      if (!dur || !isFinite(dur)) return;

      // Timeline pilotée par le scroll
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: section!,
          start: "top top",
          end: "bottom bottom",
          scrub: 1,
          // markers: true,
        },
      });

      // 1) Le scroll avance la vidéo
      tl.to(
        {},
        {
          duration: 2,
          ease: "none",
          onUpdate: () => {
            const p = tl.progress(); // 0..1
            video!.currentTime = p * dur;
            console.log(p);
          },
        },
        0
      );
    }; // <-- fermeture de init ICI ✅
    if (video!.readyState >= 1) init();
    else video!.addEventListener("loadedmetadata", init, { once: true });

    return () => {
      ScrollTrigger.getAll().forEach((s) => s.kill());
      gsap.killTweensOf([bloc, video]);
    };
  });
</script>

<!-- Intro -->
<div class="h-screen flex items-center flex-col gap-4 justify-center">
  <h1 class="text-center font-bold font-title text-5xl">
    L'histoire des contes commence ici !
  </h1>
  <p class="text-center font-light font-texte text-2xl">
    Découvrez des univers magiques où chaque conte prend vie à travers des
    illustrations captivantes et des récits enchanteurs.
  </p>
  <img src={Brand} alt="Brand Logo" class="w-64 h-auto mt-8" />
</div>

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
  </div>

  <div>
    <h1 class="text-center font-bold font-title text-5xl relative z-999">
      TEST TEST TEST TEST
    </h1>
  </div>
</section>

<!-- Suite de page -->
<div class="h-[300vh] flex items-center justify-center px-8">
  <h2 class="text-center font-semibold font-title text-4xl">
    Plongez dans un monde où l'imagination n'a pas de limites et où chaque
    histoire vous transporte vers des horizons insoupçonnés !
  </h2>
</div>
