<script>
    import { Breadcrumb, BreadcrumbItem } from 'flowbite-svelte';
    import { goto } from "$app/navigation";
</script>

<!-- Container Utama -->
<div class="flex justify-between items-center">
    <!-- Bagian Kiri (Judul dan Breadcrumb) -->
    <div class="ml-4">
        <p class="text-3xl dark:text-white font-semibold">SPMB UI-MADURA</p>
        <Breadcrumb aria-label="Default breadcrumb example">
            <BreadcrumbItem href="/" home>Home</BreadcrumbItem>
            <BreadcrumbItem href="/">Registrasi</BreadcrumbItem>
            <BreadcrumbItem>Akun</BreadcrumbItem>
        </Breadcrumb>
    </div>

    <!-- Bagian Kanan (Tombol) -->
    <div class="flex gap-2 mr-4">
        <button type="button" class="px-3 py-2 text-xs font-medium text-center text-white bg-blue-700 rounded-lg hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800">
            Setting
        </button>
        <button
            on:click={() => goto("/")}
            class="bg-red-500 text-white py-2 px-4 rounded-md hover:bg-red-600 transition-colors duration-300">
            Logout
        </button>
    </div>
</div>
