<script lang="ts">
  import Logo from "$lib/assets/logo_la_carte_des_contes_dark.png";
</script>

<section class="">
  <div
    class="w-full h-[100vh] flex items-center justify-center p-10 bg-[url('/assets/carte_zebi.png')] bg-size-[auto_800px] bg-no-repeat bg-center"
  >
    <a href="/">
      <img src={Logo} alt="" class="w-50 h-auto fixed top-10 left-10" />
    </a>
  </div>
  <div
    class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_alice.png')] bg-size-[200px] bg-center bg-no-repeat absolute bottom-50 left-100 transform -translate-x-1/2 transition-transform duration-500 hover:scale-105"
  >
    <h3 class="font-light text-3xl font-title text-center text-bg">
      Alice au Pays <br /> des Merveilles
    </h3>
  </div>
  <div
    class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_peter.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-40 right-35 transform -translate-x-1/2 transition-transform duration-500 hover:scale-105"
  >
    <h3 class="font-light text-3xl font-title text-center text-bg">
      Peter Pan
    </h3>
  </div>
  <a href="/le-petit-chaperon-rouge">
    <div
      class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_chap.png')] bg-size-[220px] bg-center bg-no-repeat absolute bottom-76 -right-2 transform -translate-x-1/2 transition-transform duration-500 hover:scale-105"
    >
      <h3 class="font-light text-3xl font-title text-center text-bg">
        Le Petit <br /> Chaperon Rouge
      </h3>
    </div></a
  >
  <div
    class="p-10 w-1/3 mx-auto text-center bg-[url('/assets/button_home_barbe.png')] bg-size-[200px] bg-center bg-no-repeat absolute top-70 left-135 transform -translate-x-1/2 transition-transform duration-500 hover:scale-105"
  >
    <h3 class="font-light text-3xl font-title text-center text-bg">
      Barbe Bleue
    </h3>
  </div>
</section>
