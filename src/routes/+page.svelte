<script lang="ts">
  import Logo from "$lib/assets/logo_la_carte_des_contes_dark.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { browser } from "$app/environment";

  let logo: HTMLDivElement | null = null;
  let bgEl: HTMLDivElement | null = null;
  let btn1: HTMLDivElement | null = null;
  let btn2: HTMLDivElement | null = null;
  let btn3: HTMLDivElement | null = null;
  let btn4: HTMLDivElement | null = null;

  onMount(() => {
    if (!browser) return;

    const tl = gsap.timeline({
      defaults: { duration: 0.3, ease: "power3.out" },
    });

    // fade-in du background
    tl.to(bgEl, { opacity: 1, delay: 0.3 });
    const buttons = [btn1, btn2, btn3, btn4];

    tl.to(buttons, { opacity: 1, stagger: 0.1 }, "-=0.2").to(
      logo,
      { opacity: 1 },
      "-=0.1"
    );
  });
</script>

<section class="">
  <div
    bind:this={bgEl}
    class="w-full h-[100vh] flex items-center justify-center p-10 opacity-0 transition-opacity bg-[url('/assets/carte_zebi.png')] bg-size-[1200px] bg-center bg-no-repeat"
  >
    <a href="/">
      <img
        bind:this={logo}
        src={Logo}
        alt=""
        class="w-50 h-auto fixed top-10 left-10 opacity-0 transition-opacity"
      />
    </a>
  </div>
  <a href="alice-au-pays-des-merveilles" class="z-999">
    <div
      bind:this={btn1}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_alice.png')] bg-size-[200px] bg-center bg-no-repeat absolute bottom-50 left-100 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Alice au Pays <br /> des Merveilles
      </h3>
    </div>
  </a>
  <a href="peter-pan" class="z-999">
    <div
      bind:this={btn2}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_peter.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-40 right-35 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Peter Pan
      </h3>
    </div>
  </a>
  <a href="le-petit-chaperon-rouge" class="z-999">
    <div
      bind:this={btn3}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_chap.png')] bg-size-[220px] bg-center bg-no-repeat absolute bottom-80 right-0 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Le Petit <br /> Chaperon Rouge
      </h3>
    </div></a
  >
  <a href="barbe-bleue" class="z-999">
    <div
      bind:this={btn4}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_barbe.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-70 left-145 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Barbe Bleue
      </h3>
    </div>
  </a>
</section>
