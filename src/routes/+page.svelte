<script lang="ts">
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import { browser } from "$app/environment";

  let section: HTMLElement | null = null;
  let video: HTMLVideoElement | null = null;

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
          duration: 2, // adapte selon ton scroll total
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
