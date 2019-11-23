<script>
  // Svelte import
  import { onMount } from "svelte";

  // Screens
  import Home from "./Home.svelte";
  import Hello from './Hello.svelte';
  import NotFound from "./NotFound.svelte";
  import Loading from './Loading.svelte';

  import rlite from "rlite-router";

  import { appRoute } from './store';

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

  $: {
    runRouter($appRoute);
  }
</script>

<svelte:component this={screen} {route} />