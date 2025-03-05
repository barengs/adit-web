<script>
    import {
      Navbar,
      NavBrand,
      NavLi,
      NavUl,
      NavHamburger,
    } from "flowbite-svelte";
  </script>
  
  <Navbar let:hidden let:toggle>
    <NavBrand href="/">
      <img
        src="https://flowbite.com/docs/images/logo.svg"
        class="mr-3 h-6 sm:h-9"
        alt="Flowbite Logo"
      />
      <span
        class="self-center whitespace-nowrap text-xl font-semibold dark:text-white"
      >
        Sistem Penerimaan Mahasiswa Baru
      </span>
    </NavBrand>
    <NavHamburger on:click={toggle} />
    <NavUl {hidden}>
      <NavLi href="/" activeClass="active" class="font-semibold">Beranda</NavLi>
      <NavLi href="/edaran" class="font-semibold">Surat Edaran</NavLi>
      <NavLi href="/informasi" class="font-semibold">Sistem Informasi</NavLi>
    </NavUl>
  </Navbar>
  