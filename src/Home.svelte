<script>
  let name;

  function sayHello () {
    if (name) {
      location.hash = `#hello/${name.split(' ')[0]}`;
    }
  }
</script>

<style>
  a {
    display: block;
  }
</style>

<h1>Welcome to my app!</h1>


<form on:submit|preventDefault={sayHello}>
  <input bind:value={name} placeholder="Name">
  <button>Say hello</button>
</form>