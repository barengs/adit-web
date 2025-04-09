<script>
  import Alerts from "$lib/components/Alerts.svelte";
  import Navbar from "$lib/components/Navbar.svelte";
</script>

<main class="min-h-screen overflow-hidden">
  <Navbar /> 

  <div class="mx-4 mt-2">
    <Alerts />
  </div>

  <div class="mx-4 mt-2 mb-6">
    <slot />
  </div>
</main>

<style>
  :global(html), :global(body) {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
  }
</style>
