<script>
  import Router from "svelte-spa-router";
  import Home from "./pages/Home.svelte";
  import League from "./pages/League.svelte";
  import Codm from "./pages/Codm.svelte";
  
</script>

<video
  src="https://assets.contentstack.io/v3/assets/blt2ac872571a60ee02/blt0f1e914c32b8fa5c/618d756b00783f138785e1a6/background-video-d-04.mp4"
  loop
  autoplay
  muted
></video>
<Router routes={{
  '/': Home,
  '/league': League,
  '/codm': Codm,
}} />


<style>
  video {
    position: fixed;
    top: 0;
    right: 0;
    z-index: -1;
    min-width: 100%;
    min-height: 100svh;
    max-width: unset;
  }
</style>
