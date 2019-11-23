<script>
  export let route = {};
</script>

{#if route.params && route.params.name}
  <h1>Hello, {route.params.name}!</h1>
{:else}
  <h1>Hello!</h1>
{/if}