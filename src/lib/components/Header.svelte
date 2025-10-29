<script>
  import { onMount } from "svelte";
  import { gsap } from "gsap";
  import { ScrollToPlugin } from "gsap/ScrollToPlugin";
  import { Observer } from "gsap/Observer";
  import logo from "$lib/assets/brand-la-carte-des-contes.png";
  import Arrow from "$lib/assets/arrow-header.png";

  gsap.registerPlugin(Observer);
  onMount(() => {
    const header = document.querySelector("#header");
    if (!header) return;

    // Position initiale : caché sur le côté gauche
    gsap.set(header, { x: -250 });
    let open = false; // état du header (fermé au départ)

    Observer.create({
      type: "wheel,touch,pointer", // écoute clic + scroll
      target: header,

      // 👇 Toggle au clic
      onClick() {
        open = !open; // inverse l'état
        gsap.to(header, {
          duration: 1,
          x: open ? 0 : -250, // si open -> visible, sinon -> caché
          ease: "power2.inOut",
        });
      },

      // 👇 Optionnel : si tu veux une réaction au scroll
      onDown() {
        if (open) {
          gsap.to(header, {
            duration: 0.8,
            x: -250,
            ease: "power2.inOut",
          });
          open = false;
        }
      },
      onUp() {
        if (!open) {
          gsap.to(header, {
            duration: 0.8,
            x: 0,
            ease: "power2.out",
          });
          open = true;
        }
      },
    });
  });
</script>

<header id="header" class="fixed w-1/4 h-auto w-mx-auto top-50 z-999">
  <nav class="flex flex-col bg-blue-400 rounded-2xl p-4 gap-6 items-start">
    <div>
      <img src={logo} alt="La Carte des Contes" class="h-10" />
    </div>
    <div class="flex items-center">
      <div class="flex flex-col gap-4 mr-25">
        <a
          href=""
          class="font-bold transition-all ease-in 0.7 hover:text-hover-text"
          >Origine des contes</a
        >
        <a
          href=""
          class="font-bold transition-all ease-in 0.7 hover:text-hover-text"
          >Bibliothèque interactive</a
        >
        <a
          href=""
          class="font-bold transition-all ease-in 0.7 hover:text-hover-text"
          >Contexte</a
        >
        <a
          href=""
          class="font-bold transition-all ease-in 0.7 hover:text-hover-text"
          >Créer ton propre compte</a
        >
      </div>
      <div class="flex items-center justify-center">
        <img src={Arrow} alt="Arrow" class="w-10 h-auto absolute top-28" />
      </div>
    </div>
  </nav>
</header>
