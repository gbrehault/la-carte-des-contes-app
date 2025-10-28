<script>
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";

  // Important: gsap and its ScrollTrigger plugin rely on the browser (window/document).
  // Import and register them only on the client inside onMount to avoid SSR errors
  // that would cause a 500 in production.
  onMount(async () => {
    const { gsap } = await import("gsap");
    const { ScrollTrigger } = await import("gsap/ScrollTrigger");
    gsap.registerPlugin(ScrollTrigger);

    const bloc = document.querySelector("#bloc-video");
    if (!bloc) return;

    // gsap.context() pour un cleanup automatique
    const ctx = gsap.context(() => {
      gsap.fromTo(
        bloc,
        { scale: 0.95, transformOrigin: "center center" },
        {
          scale: 1,
          scrollTrigger: {
            trigger: bloc,
            start: "top bottom", // démarre tôt
            end: "bottom top", // finit tard → animation plus longue
            scrub: 5, // lissage (2s)
            markers: false,
            // pin: true,           // optionnel: colle la section pour un effet narratif
          },
        }
      );
      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: bloc,
          start: "top bottom",
          end: "bottom top",
          scrub: 2,
        },
      });
      tl.to(bloc, { scale: 1 }).to(bloc, { scale: 0.95 });
    });

    return () => ctx.revert();
  });
</script>

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

<div
  id="bloc-video"
  class="w-full h-screen relative overflow-hidden px-8"
  style="will-change: transform;"
>
  <!-- 🎥 La vidéo de fond -->
  <iframe
    class="absolute inset-0 w-full h-full rounded-2xl"
    src="https://www.youtube.com/embed/8y9QnS_tMkY?autoplay=1&mute=1&loop=1&controls=0&playsinline=1&playlist=8y9QnS_tMkY"
    title="Vidéo"
    frameborder="0"
    allow="autoplay; encrypted-media; picture-in-picture"
    allowfullscreen
  ></iframe>
</div>

<div class="h-[300vh] flex items-center justify-center px-8">
  <h2 class="text-center font-semibold font-title text-4xl">
    Plongez dans un monde où l'imagination n'a pas de limites et où chaque
    histoire vous transporte vers des horizons insoupçonnés !
  </h2>
</div>
