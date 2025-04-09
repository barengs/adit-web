<script>
    import NavbarDua from "$lib/components/NavbarDua.svelte";
    import Sidebar from "$lib/components/Sidebar.svelte";
    import "flowbite";
</script>
  
<div class="flex  min-h-screen bg-gray-200"> 
    
    <div class="w-64 fixed h-full ">
      <Sidebar />
    </div>
  
    
    <div class="flex flex-col flex-1 ml-64">
      
      <div class="w-full">
        <NavbarDua />
      </div>
  
      
      <main class="p-4">
        <slot></slot>
      </main>
    </div>
</div>
