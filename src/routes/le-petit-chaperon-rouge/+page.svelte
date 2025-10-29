<script lang="ts">
  import Brand from "$lib/assets/brand-la-carte-des-contes.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollTrigger } from "gsap/ScrollTrigger";
  import { browser } from "$app/environment";
  import { Volume2, VolumeX } from "lucide-svelte";
  import IconDragon from "$lib/assets/Icon_dragon_gris.png";
  import endImage from "$lib/assets/FIN.png";
  import Illustration from "$lib/assets/Encard_illustration.png";
  import Production from "$lib/assets/Encard_production.png";
  import Design from "$lib/assets/Encard_design.png";
  import Barbe from "$lib/assets/Encard_barbe.png";
  import Alice from "$lib/assets/Encard_alice.png";
  import Peter from "$lib/assets/Encard_peter.png";
  import Footer from "$lib/components/Footer.svelte";

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
<section
  bind:this={section}
  class="relative h-[100vh] bg-[url('$lib/assets/FIGMA_TEST.1.png')] bg-cover bg-center"
>
  <!-- <div
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
    <video
      src="/video/neige_1.mov"
      muted
      playsinline
      preload="auto"
      autoplay
      class="w-full h-full absolute z-99999 object-cover"
    ></video>

    <audio bind:this={audio} src="/sound/son.2.mp3" loop></audio>

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
  </div> -->
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
      instinct et parle-en. Un adulte de confiance saura entendre et te
      protéger.
    </h3>
  </div>
  <div class="group flex items-center justify-center gap-6 cursor-pointer">
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
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="40"
      height="43"
      viewBox="0 0 40 43"
      class="transition-all duration-300"
    >
      <path
        d="M23.5436 7.20524C24.2181 7.17019 24.8995 6.73692 25.4346 6.33481C26.8333 5.28328 29.1336 2.11409 30.6688 1.73048C33.0179 1.14337 30.8004 4.67476 30.3013 5.45269C29.5128 6.67948 29.351 6.92386 28.7486 8.28306C28.5264 8.78351 27.3041 10.9158 27.7924 11.3101C28.1121 11.5681 29.3442 11.9576 29.7964 12.1075C31.2098 12.5778 32.6601 12.9429 34.1495 13.0646C34.092 13.7773 34.746 14.0499 34.2986 14.7996C33.824 15.596 32.4204 15.1092 31.6026 15.2222C30.9836 15.3069 30.2965 15.67 29.66 15.8132C29.1443 15.929 28.3821 15.9222 27.9747 16.077C27.0477 16.4285 28.0731 17.6777 28.3012 18.1791C29.003 19.7243 30.0274 21.4028 30.5567 22.9363C30.8023 23.648 31.4749 25.2983 30.6249 25.7336C29.1687 26.4794 27.8499 24.2634 26.9386 23.4348C26.5955 23.1223 26.0613 22.8866 25.7864 22.6384C25.4541 22.3385 25.3118 21.7231 24.9053 21.3765C23.3779 20.0738 23.2931 22.6053 22.9569 23.428C22.5631 24.3909 21.755 25.6411 21.3739 26.6176C21.063 27.4141 21.2375 28.2202 20.7628 29.0254C20.6575 29.2046 20.2861 29.6778 20.1243 29.7527C18.9595 30.2853 19.0229 27.5835 18.9459 27.0373C18.8835 26.5933 18.5814 26.1561 18.712 25.7131L19.0521 26.1026C19.0258 24.7307 19.1077 23.0755 18.6681 21.765C18.2967 20.657 18.0365 21.3756 17.3357 21.7095C17.0394 21.8507 16.4779 21.9393 16.2713 22.1068C16.0646 22.2742 15.972 22.798 15.782 23.0784C15.5666 23.3949 14.7303 24.1796 14.3784 24.3052C14.1903 24.3714 13.9446 24.3101 13.7906 24.3997C13.7185 24.4415 12.5976 25.4035 12.5293 25.4765C11.8227 26.2398 12.1151 25.8893 11.2837 26.3742C10.9045 26.5952 10.5565 27.1005 10.0887 27.2252C9.266 27.4442 8.65193 27.1288 8.61684 26.2496C8.54471 24.4717 9.81379 23.8622 10.6735 22.5517C11.231 21.7008 11.5225 20.5889 11.9903 19.8752C12.5839 18.9716 14.2185 18.3115 13.237 16.8491C12.2905 16.9212 11.4211 16.4003 10.4971 16.2961C9.00185 16.1277 7.05534 16.5619 5.74825 15.5873C4.4704 14.6341 5.47241 13.7004 6.64889 13.4686C6.92473 13.4141 7.25126 13.4988 7.48422 13.4278C7.75811 13.344 7.67721 13.0461 7.8166 12.9565C7.97353 12.8562 9.06423 12.9799 9.42683 12.9341C10.037 12.8572 10.7222 12.5281 11.3324 12.4035C11.9085 12.2857 14.0957 12.1533 14.3306 11.6908C14.3462 11.1368 14.1094 10.4202 13.8316 9.94603C13.4592 9.31122 12.7915 9.03276 12.2769 8.4807C11.5137 7.66382 10.0292 5.53545 10.7671 4.43816C11.5049 3.34087 12.9056 4.77796 13.6259 5.18494C14.47 5.66203 15.4379 5.9103 16.2557 6.45262C16.7801 6.80021 17.6466 7.94228 18.2022 7.78066C18.9615 7.55964 19.3796 4.72636 19.7471 3.96303C20.0074 3.42169 20.5639 3.03807 20.7569 2.53762C21.0757 1.71587 20.6819 0.670187 21.7453 0.117161C22.5943 -0.323897 22.9666 0.575744 23.1196 1.25145C23.5524 3.16367 22.7561 5.28133 23.5446 7.20427L23.5436 7.20524ZM20.8827 11.8096C20.4518 11.8485 19.2939 12.2497 19.0083 12.5739C18.6252 13.0101 18.5521 13.8231 18.3728 14.3732C18.2295 14.8123 17.7187 15.2728 18.1768 15.633C18.5365 15.9173 19.0541 15.781 19.4186 16.0507C20.3105 15.9543 22.5085 14.8074 22.4568 13.7822C22.448 13.605 22.2346 13.4725 22.1907 13.2788C22.1283 13.0062 22.2258 12.6946 22.1517 12.4415C22.0211 11.9975 21.3164 11.7706 20.8836 11.8096H20.8827Z"
        class="fill-[#D92626] transition-all duration-300 group-hover:fill-dark"
      />
      <path
        d="M3.53234 9.67048C4.10547 9.60817 6.38046 10.317 6.90193 10.6363C7.68755 11.1173 7.15536 11.94 6.45746 12.2078C5.55975 12.5534 4.98369 12.3645 4.23316 13.1989C2.19503 15.4656 5.54025 16.9903 5.28293 19.0164C5.24492 19.3124 5.05777 19.5782 5.02171 19.8275C4.89597 20.6794 5.1104 22.3696 5.69523 23.0375C6.28006 23.7055 7.89029 24.3617 7.20117 25.5096C6.77717 26.2155 5.59484 25.8436 5.2995 26.2379C5.17084 26.4102 5.19228 26.9204 5.03535 27.2398C4.87062 27.5757 4.432 27.9057 4.31114 28.2689C4.08793 28.9407 4.42908 29.5268 4.31016 30.2162C4.22244 30.7264 3.71851 31.2463 3.55963 31.8022C3.43097 32.255 3.42122 32.7632 3.33252 33.2306C3.2526 33.6512 2.94849 34.0416 3.0869 34.5031C3.26624 35.099 6.6563 36.4893 7.40683 37.0034C8.05599 37.4484 8.57259 38.0092 9.27536 38.4473C10.0815 38.9507 11.9948 40.0908 12.7034 38.9886C13.3 38.0617 12.4987 37.054 12.6284 36.0892C12.6966 35.579 13.1294 35.1438 13.1976 34.7124C13.3136 33.988 12.9539 33.2276 13.027 32.6026C13.1001 31.9775 13.6343 31.4537 13.6957 30.8286C13.7513 30.2668 13.7474 28.8774 13.4832 28.4023C13.3273 28.1229 12.8896 27.9651 12.9091 27.6185C12.9315 27.2203 14.3497 25.4035 14.8176 25.3275C15.5915 25.2019 16.6062 25.9974 17.0565 26.5855C18.2476 28.1414 16.6062 28.1306 15.8986 28.7431C15.4122 29.1637 15.8976 30.5638 15.9327 31.2132C15.9678 31.8626 15.996 32.477 15.727 33.0504C15.5516 33.4233 15.1149 33.8031 15.0593 34.2402C14.9969 34.7309 15.3976 35.1068 15.497 35.5439C15.7738 36.7649 14.6685 37.904 15.0028 39.1532C15.3069 39.5855 16.5029 38.6888 16.8567 38.5583C17.4201 38.3509 18.0225 38.3976 18.5664 38.2214C19.2837 37.9897 19.7399 37.2527 20.4505 36.9878C21.2 36.7074 22.205 36.8924 22.8073 36.3238C23.0422 36.1018 23.9741 34.3376 24.0209 34.0299C24.1271 33.3328 23.5842 32.9034 23.6319 32.0865C23.6651 31.5247 24.015 31.1548 24.1008 30.704C24.2538 29.9007 23.7704 29.0098 23.6485 28.1832C23.4662 26.9467 23.3405 25.8776 24.0443 24.8057C24.6661 23.8573 24.9819 23.5166 25.9771 24.2994C26.8017 24.9488 28.0191 26.604 28.9052 27.0217C29.0718 27.1005 30.3156 27.3761 30.5095 27.3751C31.726 27.3693 32.0106 25.679 32.6754 25.3451C33.2076 25.0773 33.7982 25.4833 34.4084 25.423C35.735 25.2915 36.4641 22.4758 36.5996 21.3775C36.7165 20.4321 36.6269 19.4195 36.8198 18.4819C36.9329 17.9367 37.3618 17.1295 37.3754 16.596C37.3979 15.7012 35.8081 14.4004 35.9329 13.7101C36.1249 12.643 38.2312 12.718 38.9896 13.2476C41.4741 14.9846 38.5578 18.146 38.8512 20.2987C38.8999 20.659 39.1592 20.9861 39.1319 21.3668C39.0978 21.8409 38.4223 22.5215 38.2312 23.1038C38.0295 23.7152 37.9028 24.6392 37.9622 25.2769C38.0109 25.8085 38.3404 26.2457 38.3589 26.7383C38.3696 27.0207 38.2546 27.2495 38.2537 27.5075C38.2517 29.2815 38.664 31.2774 38.9515 33.0495C39.0958 33.9374 39.5081 34.8809 39.4165 35.7776C39.3902 36.0376 39.2586 36.2897 39.2332 36.5672C39.1387 37.6032 39.6339 38.9458 39.3034 39.8503C38.8862 40.9943 37.3784 39.935 36.5411 39.8386C35.6151 39.7315 34.4737 39.8435 33.538 39.7228C33.0194 39.6556 32.4512 39.2856 31.9463 39.1717C31.2737 39.0198 30.646 39.2213 29.9666 39.1035C29.4364 39.011 28.9607 38.644 28.4158 38.5106C26.481 38.0374 21.6445 38.6216 20.0811 39.9282C19.7779 40.1814 19.6259 40.4978 19.3403 40.7461C18.4133 41.5513 17.0945 41.7139 15.959 42.042C15.188 42.2649 14.4667 42.7313 13.645 42.6524C12.9364 42.5853 12.4841 42.1228 11.8642 41.8998C10.8057 41.5191 8.31527 41.2738 7.54719 40.4676C7.34055 40.2505 7.39221 40.0635 7.2655 39.8727C7.06179 39.5631 4.5285 38.7472 3.95049 38.5106C3.37249 38.274 1.65406 37.6294 1.26515 37.2984C0.773896 36.8846 -0.0448654 34.8137 0.00192098 34.1682C0.0633281 33.325 0.864544 32.9024 0.997105 32.2628C1.12967 31.6231 0.883064 30.9308 1.13746 30.261C1.29927 29.8355 1.66479 29.6894 1.88117 29.3487C2.39192 28.5444 2.3773 27.0431 2.60831 26.0831C2.83932 25.1231 3.33935 24.3753 3.25942 23.3296C3.2331 22.983 3.05473 22.613 3.07227 22.2703C3.09372 21.8565 3.44657 21.284 3.44072 20.8926C3.43389 20.3922 2.92997 19.955 2.76914 19.5363C2.4621 18.7428 2.64437 17.9075 2.57809 17.0984C2.43189 15.3293 0.507798 9.99957 3.53331 9.67146L3.53234 9.67048ZM27.1127 27.193C26.4684 27.3809 26.4615 28.6058 26.3105 29.1179C26.1964 29.5025 25.8338 30.0107 25.7831 30.3437C25.674 31.0632 26.2286 31.5793 26.2695 32.2813C26.3261 33.2607 25.2276 34.3454 25.9313 35.1496C26.2471 35.5108 28.0688 36.0405 28.5806 36.1057C29.3379 36.2031 30.1226 35.91 30.7932 36.0375C30.9872 36.0745 31.1109 36.2488 31.3088 36.3014C32.4161 36.5974 33.6939 36.909 34.8236 37.0745C35.4474 37.165 36.1483 37.3296 36.7516 37.1144C37.2273 36.7395 36.3783 34.7514 36.3617 34.101C36.353 33.768 36.4894 33.4555 36.4972 33.1605C36.5284 31.9531 36.3286 29.9533 36.0011 28.7917C35.5167 27.0752 33.6189 28.1881 32.4629 28.042C32.0428 27.9895 31.5905 27.6536 31.1636 27.5874C30.6986 27.5153 30.1869 27.6321 29.7473 27.5416C29.4822 27.4871 29.2405 27.2271 28.9393 27.1804C28.6625 27.1375 27.3437 27.1268 27.1136 27.194L27.1127 27.193Z"
        class="fill-[#D92626] stroke-[#D92626] transition-all duration-300 group-hover:fill-dark group-hover:stroke-dark"
      />
    </svg>
  </div>
  <div class="flex items-center justify-center pt-30 gap-10">
    <div class="group flex items-center justify-center gap-6 cursor-pointer">
      <div class="flex flex-col items-center justify-center">
        <img src={Illustration} alt="" class="w-75 h-auto relative" />
        <div class="absolute top-365">
          <h4 class="font-bold text-dark font-title text-4xl">Illustration</h4>
          <p
            class="text-center mt-2 font-regulard text-dark font-texte text-lg"
          >
            Maëlle Brard <br />Apolline Bizieau <br />Julie Capiaux <br /> Éléa Omari
          </p>
        </div>
      </div>
      <div class="flex flex-col items-center justify-center">
        <img src={Production} alt="" class="w-75 h-auto relative" />
        <div class="absolute top-365 items-center justify-center">
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
      <div class="flex flex-col items-center justify-center">
        <img src={Design} alt="" class="w-75 h-auto relative" />
        <div class="absolute top-365 items-center justify-center">
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
  <div class="flex gap-10">
    <div class="flex items-center justify-center mt-10">
      <img src={Barbe} alt="" class="w-100 h-auto" />
      <h3
        class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
      >
        Barbe Bleue
      </h3>
    </div>
  </div>
  <div class="flex gap-10">
    <div class="flex items-center justify-center mt-10">
      <img src={Alice} alt="" class="w-100 h-auto" />
      <h3
        class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
      >
        Alice au Pays des Merveilles
      </h3>
    </div>
  </div>
  <div class="flex gap-10">
    <div class="flex items-center justify-center mt-10">
      <img src={Peter} alt="" class="w-100 h-auto" />
      <h3
        class="font-regulard text-white font-title text-3xl text-center absolute mt-2"
      >
        Peter Pan
      </h3>
    </div>
  </div>
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
