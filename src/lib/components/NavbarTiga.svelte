<script lang="ts">
  import { onMount } from 'svelte';
  import { page } from '$app/stores';
  import { browser } from '$app/environment';

  import HomeSolid from 'flowbite-svelte-icons/HomeSolid.svelte';
  import UserSolid from 'flowbite-svelte-icons/UserSolid.svelte';
  import ClipboardListSolid from 'flowbite-svelte-icons/ClipboardListSolid.svelte';

  const roleRoutes = {
    admin: [
      { name: 'Profil Admin', path: '/profiladmin', icon: UserSolid },
      { name: 'Data Peserta', path: '/dataakun', icon: ClipboardListSolid }
    ],
    user: [
      { name: 'Home', path: '/home', icon: HomeSolid }
    ]
  };

  let role: string | null = null;
  let currentRoute: any = null;
  let homeRoute: any = null;

  $: if (role) {
    const routes = roleRoutes[role as keyof typeof roleRoutes] || [];
    currentRoute = routes.find(route => route.path === $page.url.pathname);
    homeRoute = role === 'admin'
      ? { name: 'Admin', path: '/profiladmin', icon: UserSolid }
      : { name: 'Home', path: '/home', icon: HomeSolid };
  }

  onMount(() => {
    if (browser) {
      role = localStorage.getItem('role');
    }
  });
</script>

{#if currentRoute}
  <nav class="flex" aria-label="Breadcrumb">
    <ol class="inline-flex items-center space-x-1 md:space-x-2 rtl:space-x-reverse">
      <li class="inline-flex items-center">
        <a
          href={homeRoute.path}
          class="inline-flex items-center text-sm font-medium text-gray-700 hover:text-blue-600"
        >
          <svelte:component this={homeRoute.icon} class="w-4 h-4 me-2" />
          {homeRoute.name}
        </a>
      </li>
      <li aria-current="page">
        <div class="flex items-center">
          <svg
            class="rtl:rotate-180 w-3 h-3 text-gray-400 mx-1"
            aria-hidden="true"
            xmlns="http://www.w3.org/2000/svg"
            fill="none"
            viewBox="0 0 6 10"
          >
            <path
              stroke="currentColor"
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="m1 9 4-4-4-4"
            />
          </svg>
          <span class="ms-1 text-sm font-medium text-gray-500 md:ms-2">
            {currentRoute.name}
          </span>
        </div>
      </li>
    </ol>
  </nav>
{/if}

<style>
  nav {
    margin-bottom: 1.25rem;
    padding: 0.5rem 0;
  }
</style>
