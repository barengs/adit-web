<script>
  import Alerts from "$lib/components/Alerts.svelte";
import Navbar from "$lib/components/Navbar.svelte";
import "../app.css";
</script>


<Navbar/>
<main class="mt-2"> 
<Alerts/>
<div class="mt-16">
    <slot></slot>
</div>
</main>