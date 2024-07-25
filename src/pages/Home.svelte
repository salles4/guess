<script>
  import { slide } from "svelte/transition";

  let gameSelect = "btn btn-primary flex flex-col h-auto p-5 bg-transparent border-2 border-white rounded text-white"
</script>

<main in:slide>
  <div
    class="flex flex-col items-center justify-evenly gap-3 min-h-[50svh] backdrop-blur-md bg-transparent text-white border-2 border-gray-900 rounded p-4"
  >
    <div class="rounded border-gray-700 border-2 w-[30vw] min-w-[300px] text-center h-[70px] text-black">
      .
    </div>
    <div class="flex gap-3 flex-wrap justify-center">
      <a class="{gameSelect}" href="./#/league">
        <img
          src="https://cmsassets.rgpub.io/sanity/images/dsfx7636/news/9eb028de391e65072d06e77f06d0955f66b9fa2c-736x316.png?auto=format&fit=fill&q=80&w=625"
          alt="league logo"
        />
        
      </a>
      <a class="{gameSelect}" href="./#/">
        <img
          src="https://www.pngall.com/wp-content/uploads/13/Valorant-Logo-PNG-Pic.png"
          alt="league logo"
        />
        </a>

      <a class="{gameSelect}" href="./#/codm">
        <img
          src="https://snapdragonproseries.com/wp-content/uploads/2023/08/codm_logo_white_medium.png"
          alt="league logo"
        />
      </a>
    </div>
  </div>
</main>

<style>
  img {
    width: 128px;
  }
</style>
