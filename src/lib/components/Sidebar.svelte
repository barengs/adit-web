<script>
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownItem, SidebarDropdownWrapper } from 'flowbite-svelte';
    import { UserCircleSolid, ClipboardListSolid, CogSolid } from 'flowbite-svelte-icons';
</script>

<Sidebar class="h-screen fixed w-64 bg-white shadow-lg overflow-y-auto">
    <SidebarWrapper>
        <SidebarGroup>
            <SidebarDropdownWrapper label="Profil" class="font-semibold">
                <svelte:fragment slot="icon">
                    <UserCircleSolid class="w-6 h-6 text-gray-500" />
                </svelte:fragment>
                <SidebarDropdownItem label="Products" />
                <SidebarDropdownItem label="Billing" />
                <SidebarDropdownItem label="Invoice" />
            </SidebarDropdownWrapper>

            <SidebarDropdownWrapper label="Registrasi" class="font-semibold">
                <svelte:fragment slot="icon">
                    <ClipboardListSolid class="w-6 h-6 text-gray-500" />
                </svelte:fragment>
                <SidebarDropdownItem label="Products" />
                <SidebarDropdownItem label="Billing" />
                <SidebarDropdownItem label="Invoice" />
            </SidebarDropdownWrapper>

            <SidebarDropdownWrapper label="Akun" class="font-semibold">
                <svelte:fragment slot="icon">
                    <CogSolid class="w-6 h-6 text-gray-500" />
                </svelte:fragment>
                <SidebarDropdownItem label="Products" />
                <SidebarDropdownItem label="Billing" />
                <SidebarDropdownItem label="Invoice" />
            </SidebarDropdownWrapper>

        </SidebarGroup>
    </SidebarWrapper>
</Sidebar>
