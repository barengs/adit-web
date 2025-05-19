<script>
    import NavbarDua from "$lib/components/NavbarDua.svelte";
    import Sidebar from "$lib/components/Sidebar.svelte";
    import "flowbite";
    import "../../app.css";
  import NavbarTiga from "$lib/components/NavbarTiga.svelte";

</script>
  
<div class="flex  min-h-screen bg-gray-200"> 
    <div class="w-64 fixed h-full ">
      <Sidebar />
    </div>
  
   
    <div class="flex flex-col flex-1 ml-64">
     
      <div class="w-full">
        <NavbarDua />
        <NavbarTiga/>
      </div>
  
      
      <main class="p-4">
        <slot></slot>
      </main>
    </div>
</div>
