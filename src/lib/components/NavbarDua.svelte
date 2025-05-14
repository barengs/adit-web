<script>
    import { Breadcrumb, BreadcrumbItem } from 'flowbite-svelte';
    import { goto } from "$app/navigation";
</script>


<div class="flex justify-between items-center">
   
    <div class="ml-4">
        <p class="text-3xl dark:text-white font-semibold">SPMB UI-MADURA</p>
        <Breadcrumb aria-label="Default breadcrumb example">
            <BreadcrumbItem href="" home>Pmb</BreadcrumbItem>
        </Breadcrumb>
    </div>

    
    <div class="flex gap-2 mr-4">
        
        <button
            on:click={() => goto("/")}
            class="bg-red-500 text-white py-2 px-4 rounded-md hover:bg-red-600 transition-colors duration-300">
            Logout
        </button>
    </div>
</div>
