<script lang="ts">
  import logo from "$lib/assets/logo_la_carte_des_contes.png";
  import { Facebook, Instagram, Linkedin, Youtube } from "lucide-svelte";
</script>

<footer class="w-full h-50 bg-[#5F5F5F] w-mx-auto">
  <nav class="flex p-4 gap-6 items-center justify-between h-full px-10">
    <div>
      <img src={logo} alt="La Carte des Contes" class="h-20" />
    </div>
    <div class="flex flex-row gap-4">
      <Facebook
        class="w-10 h-auto bg-bg p-2 rounded-xl border-color-bg border-2transition all ease-in 0.5s "
      />
      <Instagram
        class="w-10 h-auto bg-bg p-2 rounded-xl border-color-bg border-2 transition all ease-in 0.5s "
      />
      <Linkedin
        class="w-10 h-auto bg-bg p-2 rounded-xl border-color-bg border-2  transition all ease-in 0.5s "
      />
      <Youtube
        class="w-10 h-auto bg-bg p-2 rounded-xl border-color-bg border-2  transition all ease-in 0.5s "
      />
    </div>
  </nav>
</footer>
