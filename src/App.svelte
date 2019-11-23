<script>
  // Svelte import
  import { onMount } from "svelte";

  // Screens
  import Home from "./Home.svelte";
  import Hello from './Hello.svelte';
  import NotFound from "./NotFound.svelte";
  import Loading from './Loading.svelte';

  import rlite from "rlite-router";

  let route = {};
  let screen = Loading;

  function routeScreen(_screen) {
    return function(params, state, url) {
      route = {
        params,
        state,
        url
      };

      screen = _screen;
    };
  }

  const runRouter = rlite(routeScreen(NotFound), {
    "": routeScreen(Home),
    'hello/:name': routeScreen(Hello),
  });

  // Hash-based routing
  function processHash() {
    const hash = location.hash || "#";
    runRouter(hash.slice(1));
  }

  onMount(() => {
    processHash();

    window.addEventListener("hashchange", processHash);

    return () => {
      window.removeEventListener("hashchnage", processHash);
    };
  });
</script>

<svelte:component this={screen} {route} />