<script>
  import Alerts from "$lib/components/Alerts.svelte";
import Navbar from "$lib/components/Navbar.svelte";
import "../../app.css";
</script>



<main class="mt-2">
  <Navbar/> 
<Alerts/>
<div class="mt-16">
    <slot></slot>
</div>
</main>