<script>
    import { Button, Dropdown, DropdownItem, Avatar, DropdownHeader } from 'flowbite-svelte';
    import { goto } from "$app/navigation";
</script>


<div class="flex justify-between items-center bg-slate-50 h-[60px]">
   
    <div class="ml-4">
        <p class="text-3xl dark:text-white font-semibold">SPMB UI-MADURA</p>
        
    </div>

    
    <div class="flex gap-2 mr-4">
        <Button pill color='none' id="avatar_with_name" class="p-1!!border-none !shadow-none focus:ring-0 focus:outline-none" >
  <Avatar src="/images/profile-picture-3.webp" class="me-2" />
  Bonnie Green
</Button>
<Dropdown triggeredBy="#avatar_with_name">
  <DropdownHeader>
    <span class="block text-sm text-gray-900 dark:text-white">Bonnie Green</span>
    <span class="block truncate text-sm font-medium">name@flowbite.com</span>
  </DropdownHeader>
  <DropdownItem>Settings</DropdownItem>
  <DropdownItem class='hover:bg-red-600 '><button
            on:click={() => goto("/")}
            class=" text-black hover:text-white">
            Log out
        </button></DropdownItem>
      
  </Dropdown>
        
    </div>
</div>
