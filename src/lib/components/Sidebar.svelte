<script lang="ts">
    import { goto } from '$app/navigation';
    import { 
        ChevronDownOutline, 
        ChevronUpOutline, 
        HomeSolid, 
        UserSolid, 
        BookOpenSolid, 
        UsersGroupSolid, 
        ClipboardListSolid 
    } from 'flowbite-svelte-icons';
    import { onMount } from 'svelte';

    type MenuItem = {
        name: string;
        path: string;
        icon: any;
    };

    const menuItems: MenuItem[] = [
        { name: 'Home', path: '/home', icon: HomeSolid },
        { name: 'Data Akun', path: '/dataakun', icon: UserSolid },
        { name: 'Data PMB', path: '/datapmb', icon: ClipboardListSolid },
    ];

    let dropdownOpen = false;
    let activePath = '';

    onMount(() => {
        activePath = window.location.pathname;
    });

    function navigateTo(path: string) {
        goto(path);
        activePath = path;
    }

    function toggleDropdown() {
        dropdownOpen = !dropdownOpen;
    }
</script>

<div class="w-64 h-screen bg-gray-800 text-white p-5 fixed top-0 left-0">
    <h2 class="text-xl font-semibold mb-6">Sistem PMB</h2>

    <!-- Dropdown Profil -->
    <div class="mb-4">
        <button 
            class="flex items-center justify-between w-full px-4 py-2 text-left hover:bg-gray-700 rounded-md transition"
            on:click={toggleDropdown}
        >
            <span>Profil</span>
            {#if dropdownOpen}
                <ChevronUpOutline class="w-5 h-5" />
            {:else}
                <ChevronDownOutline class="w-5 h-5" />
            {/if}
        </button>
        
        {#if dropdownOpen}
            <ul class="mt-2 space-y-2">
                {#each menuItems as item}
                    <li>
                        <button 
                            on:click={() => navigateTo(item.path)}
                            class="w-full flex items-center gap-2 text-left px-6 py-2 hover:bg-gray-700 rounded-md transition"
                            class:item-active={activePath === item.path}
                        >
                            <svelte:component this={item.icon} class="w-5 h-5" />
                            {item.name}
                        </button>
                    </li>
                {/each}
            </ul>
        {/if}
    </div>
</div>
