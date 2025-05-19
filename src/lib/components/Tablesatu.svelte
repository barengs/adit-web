<script lang="ts">
  type Product = {
    id: number;
    name: string;
    nik: number;
    category: string;
    price: number;
  };

  let products: Product[] = [
    { id: 1, name: 'aldean tegar', nik: 2804358539849893, category: 'lulus', price: 2999 },
    { id: 2, name: 'miftah esteh', nik: 2804358539849893, category: 'tidak lulus', price: 1999 },
    { id: 3, name: 'Mika besi', nik: 2804358539849893, category: 'lulus', price: 99 },
    { id: 4, name: 'bika ambon', nik: 2804358539849893, category: 'lulus gess', price: 179 },
    { id: 5, name: 'azriel malikik', nik: 2804358539849893, category: 'tidak lulus', price: 699 },
    { id: 6, name: 'ramdaniar"', nik: 2804358539849893, category: 'lulus', price: 3999 }
  ];

  let searchTerm = '';
  let showModal = false;
  let showAddModal = false;
  let showDetailModal = false;
  let selectedProduct: Product | null = null;

  let newProduct: Product = {
    id: 0,
    name: '',
    nik: 0,
    category: '',
    price: 0
  };

  function openModal(product: Product) {
    selectedProduct = { ...product };
    showModal = true;
  }

  function openDetailModal(product: Product) {
    selectedProduct = { ...product };
    showDetailModal = true;
  }

  function openAddModal() {
    newProduct = { id: 0, name: '', nik: 0, category: '', price: 0 };
    showAddModal = true;
  }

  function saveChanges() {
    if (!selectedProduct) return;
    const index = products.findIndex(p => p.id === selectedProduct!.id);
    if (index !== -1) {
      products[index] = { ...selectedProduct };
    }
    showModal = false;
  }

  function addNewProduct() {
    newProduct.id = products.length + 1;
    products.push({ ...newProduct });
    showAddModal = false;
  }

  function closeModal() {
    showModal = false;
    showAddModal = false;
    showDetailModal = false;
  }

  $: filteredProducts = products.filter(p =>
    p.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
    p.category.toLowerCase().includes(searchTerm.toLowerCase())
  );

 import { onMount, onDestroy } from 'svelte';

  // Variabel untuk menyimpan id dropdown yang aktif, bisa number atau null
  let activeDropdownId: number | null = null;

  // id adalah number
  function toggleDropdown(id: number) {
    activeDropdownId = activeDropdownId === id ? null : id;
  }

  function closeDropdown() {
    activeDropdownId = null;
  }

  // event adalah MouseEvent
  function handleClickOutside(event: MouseEvent) {
    // Pilih semua elemen dropdown dan tombol toggle
    const dropdowns = document.querySelectorAll<HTMLElement>('.dropdown-menu, .dropdown-toggle');
    let isClickInside = false;

    dropdowns.forEach((dropdown) => {
      if (dropdown.contains(event.target as Node)) {
        isClickInside = true;
      }
    });

    if (!isClickInside) {
      closeDropdown();
    }
  }

  onMount(() => {
    window.addEventListener('click', handleClickOutside);
  });

  onDestroy(() => {
    window.removeEventListener('click', handleClickOutside);
  });
</script>


<div class="flex justify-between items-center mb-4">
  <div class="mb-4 w-60">
    <input
      type="text"
      placeholder="Cari nama"
      bind:value={searchTerm}
      class="w-full p-2 rounded-lg text-gray-500 bg-white border-none focus:ring-2 focus:ring-blue-500"
    />
  </div>

  <button
    class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
    on:click={openAddModal}
  >
    Tambah Peserta
  </button>
</div>


<div class="overflow-x-auto">
  <table class="min-w-full bg-white dark:bg-gray-800">
    <thead>
      <tr>
        <th class="px-6 py-3 text-left text-black-500 tracking-wider">NAMA</th>
        <th class="px-6 py-3 text-left text-black-500 tracking-wider">NIK</th>
        <th class="px-6 py-3 text-left text-black-500 tracking-wider">STATUS</th>
        <th class="px-6 py-3 text-left text-black-500 tracking-wider">TTL</th>
       
      </tr>
    </thead>
    <tbody class="bg-white dark:bg-gray-700">
      {#each filteredProducts as product}
        <tr class="hover:bg-gray-100 dark:hover:bg-gray-600">
          <td class="px-6 py-4 whitespace-nowrap">{product.name}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.nik}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.category}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.price}</td>
         <td class="relative px-6 py-4 whitespace-nowrap">
  <button
    class="dropdown-toggle text-gray-600 hover:text-black text-xl font-bold focus:outline-none"
    on:click={(e) => {
      e.stopPropagation();
      toggleDropdown(product.id);
    }}
  >
    ⋮
  </button>

  {#if activeDropdownId === product.id}
    <div class="dropdown-menu absolute right-0 mt-2 w-32 bg-white border rounded shadow-md z-50">
      <button
        class="block w-full text-left px-4 py-2 hover:bg-gray-100"
        on:click={(e) => {
          e.stopPropagation();
          openDetailModal(product);
          closeDropdown();
        }}
      >
        Lihat Detail
      </button>
      <button
        class="block w-full text-left px-4 py-2 hover:bg-gray-100"
        on:click={(e) => {
          e.stopPropagation();
          openModal(product);
          closeDropdown();
        }}
      >
        Edit
      </button>
    </div>
  {/if}
</td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>


{#if showModal && selectedProduct}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Edit Peserta</h2>

      <div class="mb-4">
        <label for="edit-nama" class="block text-gray-700 dark:text-gray-300">Nama</label>
        <input id="edit-nama" type="text" bind:value={selectedProduct.name}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="edit-nik" class="block text-gray-700 dark:text-gray-300">NIK</label>
        <input id="edit-nik" type="text" bind:value={selectedProduct.nik}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="edit-status" class="block text-gray-700 dark:text-gray-300">Status</label>
        <input id="edit-status" type="text" bind:value={selectedProduct.category}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="edit-ttl" class="block text-gray-700 dark:text-gray-300">TTL</label>
        <input id="edit-ttl" type="text" bind:value={selectedProduct.price}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="flex justify-end">
        <button class="bg-gray-400 hover:bg-gray-600 text-white py-2 px-4 rounded mr-2" on:click={closeModal}>Batal</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white py-2 px-4 rounded" on:click={saveChanges}>Simpan</button>
      </div>
    </div>
  </div>
{/if}


{#if showDetailModal && selectedProduct}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Detail Peserta</h2>
      <p class="text-gray-800 dark:text-gray-200 mb-2"><strong>Nama:</strong> {selectedProduct.name}</p>
      <p class="text-gray-800 dark:text-gray-200 mb-2"><strong>NIK:</strong> {selectedProduct.nik}</p>
      <p class="text-gray-800 dark:text-gray-200 mb-2"><strong>Status:</strong> {selectedProduct.category}</p>
      <p class="text-gray-800 dark:text-gray-200 mb-4"><strong>TTL:</strong> {selectedProduct.price}</p>
      <div class="flex justify-end">
        <button class="bg-gray-500 hover:bg-gray-700 text-white py-2 px-4 rounded" on:click={closeModal}>Tutup</button>
      </div>
    </div>
  </div>
{/if}


{#if showAddModal}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Tambah Peserta</h2>

      <div class="mb-4">
        <label for="add-nama" class="block text-gray-700 dark:text-gray-300">Nama</label>
        <input id="add-nama" type="text" bind:value={newProduct.name}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="add-nik" class="block text-gray-700 dark:text-gray-300">NIK</label>
        <input id="add-nik" type="text" bind:value={newProduct.nik}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="add-status" class="block text-gray-700 dark:text-gray-300">Status</label>
        <input id="add-status" type="text" bind:value={newProduct.category}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="add-ttl" class="block text-gray-700 dark:text-gray-300">TTL</label>
        <input id="add-ttl" type="text" bind:value={newProduct.price}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="flex justify-end">
        <button class="bg-gray-400 hover:bg-gray-600 text-white py-2 px-4 rounded mr-2" on:click={closeModal}>Batal</button>
        <button class="bg-green-500 hover:bg-green-700 text-white py-2 px-4 rounded" on:click={addNewProduct}>Tambah</button>
      </div>
    </div>
  </div>
{/if}
