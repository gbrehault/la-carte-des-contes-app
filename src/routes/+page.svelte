<script lang="ts">
  import Logo from "$lib/assets/logo_la_carte_des_contes_dark.png";
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { browser } from "$app/environment";
  import Carte from "$lib/assets/carte/carte.png";
  import Montagne from "$lib/assets/carte/Montagne.png";
  import Chateau from "$lib/assets/carte/Chateau_2.png";
  import Arbres from "$lib/assets/carte/Arbres.png";
  import Montagne2 from "$lib/assets/carte/Montagne_2.png";
  import Dragon from "$lib/assets/carte/Dragon.png";
  import Bateau from "$lib/assets/carte/Bateau.png";
  import Dragon2 from "$lib/assets/carte/Dragon_2.png";
  import Village from "$lib/assets/carte/Village.png";
  import Chateau2 from "$lib/assets/carte/Chateau_1.png";
  import Oiseau from "$lib/assets/carte/Oiseau.png";

  let logo: HTMLDivElement | null = null;
  let bgEl: HTMLDivElement | null = null;
  let btn1: HTMLDivElement | null = null;
  let btn2: HTMLDivElement | null = null;
  let btn3: HTMLDivElement | null = null;
  let btn4: HTMLDivElement | null = null;
  let ico1: HTMLDivElement | null = null;
  let ico2: HTMLDivElement | null = null;
  let ico3: HTMLDivElement | null = null;
  let ico4: HTMLDivElement | null = null;
  let ico5: HTMLDivElement | null = null;
  let ico6: HTMLDivElement | null = null;
  let ico7: HTMLDivElement | null = null;
  let ico8: HTMLDivElement | null = null;
  let ico9: HTMLDivElement | null = null;
  let ico10: HTMLDivElement | null = null;
  let ico11: HTMLDivElement | null = null;

  onMount(() => {
    if (!browser) return;

    const tl = gsap.timeline({
      defaults: { duration: 0.3, ease: "power3.out" },
    });

    // fade-in du background
    tl.to(bgEl, { opacity: 1, delay: 0.3 });

    // fade-in groupé des icônes et boutons
    const icons = [
      ico1,
      ico2,
      ico3,
      ico4,
      ico5,
      ico6,
      ico7,
      ico8,
      ico9,
      ico10,
      ico11,
    ];
    const buttons = [btn1, btn2, btn3, btn4];

    tl.to(icons, { opacity: 1, stagger: 0.3 }, "-=0.1")
      .to(buttons, { opacity: 1, stagger: 0.1 }, "-=0.2")
      .to(logo, { opacity: 1 }, "-=0.1");
  });
</script>

<section class="">
  <div
    bind:this={bgEl}
    class="w-full h-[100vh] flex items-center justify-center p-10 opacity-0 transition-opacity"
  >
    <img
      bind:this={ico1}
      src={Carte}
      alt=""
      class="w-280 h-full object-contain absolute left-25 top-4 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico2}
      src={Montagne}
      alt=""
      class="w-70 h-full object-contain absolute left-35 bottom-22 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico3}
      src={Chateau}
      alt=""
      class="w-80 h-full object-contain absolute left-40 -bottom-10 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico4}
      src={Arbres}
      alt=""
      class="w-60 h-full object-contain absolute left-120 -bottom-10 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico5}
      src={Montagne2}
      alt=""
      class=" w-50 h-full object-contain absolute left-120 bottom-48 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico6}
      src={Dragon}
      alt=""
      class=" w-50 h-full object-contain absolute right-30 top-0 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico7}
      src={Bateau}
      alt=""
      class=" w-40 h-full object-contain absolute right-130 bottom-86 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico8}
      src={Dragon2}
      alt=""
      class=" w-50 h-full object-contain absolute right-150 bottom-20 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico9}
      src={Village}
      alt=""
      class=" w-80 h-full object-contain absolute right-120 top-30 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico10}
      src={Chateau2}
      alt=""
      class=" w-50 h-full object-contain absolute right-110 bottom-40 opacity-0 transition-opacity"
    />
    <img
      bind:this={ico11}
      src={Oiseau}
      alt=""
      class=" w-20 h-full object-contain absolute left-70 bottom-60 opacity-0 transition-opacity"
    />
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
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_peter.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-40 right-55 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Peter Pan
      </h3>
    </div>
  </a>
  <a href="le-petit-chaperon-rouge" class="z-999">
    <div
      bind:this={btn3}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_chap.png')] bg-size-[220px] bg-center bg-no-repeat absolute bottom-85 right-2 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Le Petit <br /> Chaperon Rouge
      </h3>
    </div></a
  >
  <a href="barbe-bleue" class="z-999">
    <div
      bind:this={btn4}
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_barbe.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-70 left-135 transform -translate-x-1/2 duration-500 hover:scale-105 opacity-0 transition"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Barbe Bleue
      </h3>
    </div>
  </a>
</section>
