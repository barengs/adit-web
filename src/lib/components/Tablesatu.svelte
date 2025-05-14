<script lang="ts">
  import ModalAdmin from "./ModalAdmin.svelte";

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
  let selectedProduct: Product | null = null;

  // New product to add
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

  function openAddModal() {
    newProduct = { id: 0, name: '', nik: 0, category: '', price: 0 };  // Reset new product
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
    newProduct.id = products.length + 1; // Simple way to create a unique ID for the new product
    products.push({ ...newProduct });
    showAddModal = false;
  }

  function closeModal() {
    showModal = false;
    showAddModal = false;
  }

  $: filteredProducts = products.filter(p =>
    p.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
    p.category.toLowerCase().includes(searchTerm.toLowerCase())
  );

</script>

<div class="flex justify-between items-center mb-4">
  <div class="mb-4 w-60">
    <input
      type="text"
      placeholder="Cari nama"
      bind:value={searchTerm}
      class="w-full p-2 rounded-lg text-gray-500 bg-transparent border-none focus:ring-2 focus:ring-blue-500 bg-white"
    />
  </div>

   <button
    class="bg-green-500 hover:bg-green-700 text-white font-bold py-2 px-4 rounded"
    on:click={openAddModal}
  >
    tambah Peserta
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
        <th class="px-6 py-3"></th>
      </tr>
    </thead>
    <tbody class="bg-white dark:bg-gray-700">
      {#each filteredProducts as product}
        <tr class="hover:bg-gray-100 dark:hover:bg-gray-600">
          <td class="px-6 py-4 whitespace-nowrap">{product.name}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.nik}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.category}</td>
          <td class="px-6 py-4 whitespace-nowrap">{product.price}</td>
          <td class="px-6 py-4 whitespace-nowrap">
            <button
              class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-1 px-4 rounded"
              on:click={() => openModal(product)}
            >
              Edit
            </button>
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

{#if showModal && selectedProduct}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Edit Product</h2>

      <div class="mb-4">
        <label for="product-name" class="block text-gray-700 dark:text-gray-300">nama</label>
        <input id="product-name" type="text" bind:value={selectedProduct.name}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="product-nik" class="block text-gray-700 dark:text-gray-300">nik</label>
        <input id="product-nik" type="text" bind:value={selectedProduct.nik}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="product-category" class="block text-gray-700 dark:text-gray-300">ttl</label>
        <input id="product-category" type="text" bind:value={selectedProduct.category}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="product-price" class="block text-gray-700 dark:text-gray-300">Price</label>
        <input id="product-price" type="text" bind:value={selectedProduct.price}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="flex justify-end">
        <button class="bg-gray-400 hover:bg-gray-600 text-white py-2 px-4 rounded mr-2" on:click={closeModal}>Cancel</button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white py-2 px-4 rounded" on:click={saveChanges}>Save</button>
      </div>
    </div>
  </div>
{/if}

{#if showAddModal}
  <div class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
    <div class="bg-white dark:bg-gray-800 p-8 rounded-lg shadow-lg w-full max-w-md">
      <h2 class="text-xl font-bold mb-4 text-gray-800 dark:text-gray-200">Add New Product</h2>

      <div class="mb-4">
        <label for="new-product-name" class="block text-gray-700 dark:text-gray-300">nama</label>
        <input id="new-product-name" type="text" bind:value={newProduct.name}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="new-product-nik" class="block text-gray-700 dark:text-gray-300">nik</label>
        <input id="new-product-nik" type="text" bind:value={newProduct.nik}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="new-product-category" class="block text-gray-700 dark:text-gray-300">status</label>
        <input id="new-product-category" type="text" bind:value={newProduct.category}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="mb-4">
        <label for="new-product-price" class="block text-gray-700 dark:text-gray-300">ttl</label>
        <input id="new-product-price" type="text" bind:value={newProduct.price}
          class="w-full p-2 mt-1 rounded dark:bg-gray-700 dark:text-white focus:outline-none" />
      </div>

      <div class="flex justify-end">
        <button class="bg-gray-400 hover:bg-gray-600 text-white py-2 px-4 rounded mr-2" on:click={closeModal}>Cancel</button>
        <button class="bg-green-500 hover:bg-green-700 text-white py-2 px-4 rounded" on:click={addNewProduct}>Add</button>
      </div>
    </div>
  </div>
{/if}
