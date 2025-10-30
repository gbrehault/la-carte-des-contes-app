<script lang="ts">
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import Logo from "$lib/assets/logo-site.png";
  import { browser } from "$app/environment";
  import { Volume2, VolumeX } from "lucide-svelte";
  import IconDragon from "$lib/assets/Icon_dragon_gris.png";
  import endImage from "$lib/assets/FIN.png";
  import Barbe from "$lib/assets/Encard_barbe.png";
  import Alice from "$lib/assets/Encard_alice.png";
  import Peter from "$lib/assets/Encard_peter.png";
  import Footer from "$lib/components/Footer.svelte";

  let section: HTMLElement | null = null;
  let video: HTMLVideoElement | null = null;
  let audio: HTMLAudioElement | null = null;
  let isPlaying = false;
  let isSafari = false;

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
    if (!browser) return;
    // Détection basique de Safari (Mac + iOS)
    isSafari =
      /^((?!chrome|android).)*safari/i.test(navigator.userAgent) ||
      /iPad|iPhone|iPod/.test(navigator.userAgent);

    gsap.registerPlugin(ScrollTrigger);

    if (!section || !video) return;

    const init = () => {
      const dur = video!.duration;
      if (!dur || !isFinite(dur)) return;

      const tl = gsap.timeline({
        scrollTrigger: {
          trigger: section!,
          start: "top top",
          end: () => "+=" + (section!.scrollHeight - window.innerHeight - 1000),
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
            if (video) {
              const p = st.progress; // 0..1
              video!.currentTime = Math.min(p * dur, dur - 0.06666666);
            }
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
<section
  bind:this={section}
  class="relative h-[1000vh] bg-cover bg-center
"
>
  <a href="/">
    <img src={Logo} alt="" class="top-0 left-0 w-30 z-999 fixed" />
  </a>
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
    <!-- 🎥 WebM pour Chrome, Edge, Firefox -->
    {#if !isSafari}
      <video
        autoplay
        muted
        loop
        playsinline
        preload="auto"
        class="absolute inset-0 w-full h-full object-cover z-0"
      >
        <source src="/video/neige-final.webm" type="video/webm" />
      </video>
    {/if}

    <!-- 🎬 MOV (H.264) pour Safari (Mac + iOS) -->
    {#if isSafari}
      <video
        autoplay
        muted
        loop
        playsinline
        preload="auto"
        class="absolute inset-0 w-full h-full object-cover z-0"
      >
        <source src="/video/neige-final.mov" type="video/quicktime" />
      </video>
    {/if}

    <audio bind:this={audio} src="/sound/son.2.mp3" loop></audio>

    <button
      on:click={toggleAudio}
      class="px-5 py-3 fixed bottom-0 right-0 rounded-xl bg-red-500 m-6 text-white z-999 hover:bg-red-600 transition cursor-pointer"
    >
      {#if isPlaying}
        <Volume2></Volume2>
      {:else}
        <VolumeX></VolumeX>
      {/if}
    </button>
  </div>
  <div class="flex h-full items-center justify-center">
    <img src={endImage} alt="" class="w-150 h-auto" />
  </div>
</section>
<section class="flex flex-col items-center justify-center pt-30">
  <img src={IconDragon} alt="" class="w-200 h-auto left-0 absolute -z-1" />
  <div class="flex items-center jsutfify-center my-20 px-4">
    <h3 class="font-sb text-3xl max-w-4xl text-center">
      Le loup ne porte pas toujours de crocs. Parfois, il se cache derrière des
      mots doux. Quand quelque chose te semble étrange, fais confiance à ton
      instinct et parles-en. Un adulte de confiance saura entendre et te
      protéger.
    </h3>
  </div>
  <div
    class="group flex items-center justify-center gap-6 cursor-pointer z-999"
  >
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="22"
      height="39"
      viewBox="0 0 22 39"
      fill="none"
      class="w-5 pt-2 transition-all duration-300"
    >
      <path
        d="M17.5908 1.12549L0.991211 19.1489L0.679688 19.4878L0.991211 19.8267L17.5488 37.8032L17.917 38.2026L18.2852 37.8032L20.6494 35.2349L20.9609 34.896L20.6494 34.5571L7.97168 20.7925L6.77051 19.4878L20.7275 4.3335L21.0439 3.98975L20.7217 3.65088L18.3213 1.12061L17.9531 0.731934L17.5908 1.12549Z"
        class="fill-[#D92626] stroke-[#D92626] transition-all duration-300 group-hover:fill-dark group-hover:stroke-dark"
      />
    </svg>
    <a
      href="/"
      class="font-title font-bold text-3xl pt-2 text-[#D92626] transition-colors duration-300 group-hover:text-dark"
      >RETOURNEZ À LA CARTE</a
    >
  </div>
  <div class="w-full flex items-center justify-center pt-30">
    <div
      class="group h-auto flex items-stretch justify-center gap-20 cursor-pointer"
    >
      <div
        class="w-full flex flex-col items-center justify-center bg-[url('/assets/Encard_illustration.png')] bg-cover bg-center p-10"
      >
        <div class="z-99">
          <h4 class="font-bold text-dark font-title text-4xl">Illustration</h4>
          <p
            class="text-center mt-2 font-regulard text-dark font-texte text-lg"
          >
            Maëlle Brard <br />Apolline Bizieau <br />Julie Capiaux <br /> Éléa Omari
          </p>
        </div>
      </div>
      <div
        class="w-full flex flex-col items-center justify-center bg-[url('/assets/Encard_design.png')] bg-cover bg-center p-10"
      >
        <div class="z-99">
          <h4 class="font-bold text-dark font-title text-4xl text-center">
            Production
          </h4>
          <p
            class="text-center mt-2 font-regulard text-dark font-texte text-lg"
          >
            Gabriel Brehault <br />Arthur Etcheverria <br />Léa Nemeth
          </p>
        </div>
      </div>
      <div
        class="w-full flex flex-col items-center justify-center bg-[url('/assets/Encard_production.png')] bg-cover bg-center p-10"
      >
        <div class="z-99">
          <h4 class="font-bold text-dark font-title text-4xl text-center">
            Design <br /> graphique
          </h4>
          <p
            class="text-center mt-2 font-regulard text-dark font-texte text-lg"
          >
            Charlotte Brison <br />Léna Lemonnier <br />Izia Besson
          </p>
        </div>
      </div>
    </div>
  </div>
  <h2 class="font-bold text-red font-title text-5xl text-center mt-30">
    DÉCOUVRIR NOS CONTES
  </h2>
  <a href="/barbe-bleue">
    <div
      class="flex gap-10 transform transition-transform duration-500 hover:scale-105"
    >
      <div class="flex items-center justify-center mt-10">
        <img src={Barbe} alt="" class="w-100 h-auto" />
        <h3
          class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
        >
          Barbe Bleue
        </h3>
      </div>
    </div>
  </a>
  <a href="/alice-au-pays-des-merveilles">
    <div
      class="flex gap-10 transform transition-transform duration-500 hover:scale-105"
    >
      <div class="flex items-center justify-center mt-10">
        <img src={Alice} alt="" class="w-100 h-auto" />
        <h3
          class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
        >
          Alice au Pays des Merveilles
        </h3>
      </div>
    </div>
  </a>
  <a href="/peter-pan">
    <div
      class="flex gap-10 transform transition-transform duration-500 hover:scale-105"
    >
      <div class="flex items-center justify-center mt-10">
        <img src={Peter} alt="" class="w-100 h-auto" />
        <h3
          class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
        >
          Peter Pan
        </h3>
      </div>
    </div>
  </a>
  <div class="flex flex-col items-center justify-center mt-20 mb-10 gap-2">
    <h3 class="text-dark font-regulard text-4xl font-texte">
      Les contes sont faits pour être racontés.
    </h3>
    <h3 class="text-dark font-bold text-4xl font-texte">
      Nous, on les fait vivre.
    </h3>
  </div>
</section>
<Footer />
