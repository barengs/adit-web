<script>
    import NavbarDua from "$lib/components/NavbarDua.svelte";
    import Sidebar from "$lib/components/Sidebar.svelte";
    import "flowbite";
</script>
  
<div class="flex h-screen bg-gray-200"> <!-- Tambahkan bg-gray-100 di sini -->
    <!-- Sidebar -->
    <div class="w-64 fixed h-full ">
      <Sidebar />
    </div>
  
    <!-- Konten utama -->
    <div class="flex flex-col flex-1 ml-64">
      <!-- Navbar -->
      <div class="w-full">
        <NavbarDua />
      </div>
  
      <!-- Slot untuk konten -->
      <main class="p-4">
        <slot></slot>
      </main>
    </div>
</div>
