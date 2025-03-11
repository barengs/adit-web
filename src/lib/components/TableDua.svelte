<script lang="ts">
  import { onMount } from 'svelte';

  // Data produk
  let products = [
    { id: 1, name: 'Apple iMac 27"', category: 'PC', brand: 'Apple', description: '300', price: '$2999' },
    { id: 2, name: 'Apple iMac 20"', category: 'PC', brand: 'Apple', description: '200', price: '$1499' },
    { id: 3, name: 'Apple iPhone 14', category: 'Phone', brand: 'Apple', description: '1237', price: '$999' },
    { id: 4, name: 'Apple iPad Air', category: 'Tablet', brand: 'Apple', description: '4578', price: '$1199' },
    { id: 5, name: 'Xbox Series S', category: 'Gaming/Console', brand: 'Microsoft', description: '56', price: '$299' },
    { id: 6, name: 'PlayStation 5', category: 'Gaming/Console', brand: 'Sony', description: '78', price: '$799' },
    { id: 7, name: 'Xbox Series X', category: 'Gaming/Console', brand: 'Microsoft', description: '200', price: '$699' },
    { id: 8, name: 'Apple Watch SE', category: 'Watch', brand: 'Apple', description: '657', price: '$399' },
    { id: 9, name: 'NIKON D850', category: 'Photo', brand: 'Nikon', description: '465', price: '$599' },
    { id: 10, name: 'Monitor BenQ EX2710Q', category: 'TV/Monitor', brand: 'BenQ', description: '354', price: '$499' },
  ];

  // State untuk pencarian
  let searchTerm = '';

  // Fungsi untuk memfilter produk berdasarkan pencarian
  $: filteredProducts = products.filter(product =>
    product.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  // Fungsi untuk menangani dropdown
  function toggleDropdown(id: string) {
    const dropdown = document.getElementById(id);
    dropdown?.classList.toggle('hidden');
  }

  // Tutup dropdown saat klik di luar
  onMount(() => {
    document.addEventListener('click', (event) => {
      const dropdowns = document.querySelectorAll('.dropdown');
      dropdowns.forEach((dropdown) => {
        if (!dropdown.contains(event.target as Node)) {
          dropdown.classList.add('hidden');
        }
      });
    });
  });
</script>

<section class="bg-gray-50 dark:bg-gray-900 p-3 sm:p-5">
  <div class="mx-auto max-w-screen-xl px-4 lg:px-12">
    <div class="bg-white dark:bg-gray-800 relative shadow-md sm:rounded-lg overflow-hidden">
      <!-- Header dengan Pencarian dan Tombol -->
      <div class="flex flex-col md:flex-row items-center justify-between space-y-3 md:space-y-0 md:space-x-4 p-4">
        <div class="w-full md:w-1/2">
          <form class="flex items-center" on:submit|preventDefault>
            <label for="simple-search" class="sr-only">Search</label>
            <div class="relative w-full">
              <div class="absolute inset-y-0 left-0 flex items-center pl-3 pointer-events-none">
                <svg class="w-5 h-5 text-gray-500 dark:text-gray-400" fill="currentColor" viewBox="0 0 20 20">
                  <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
                </svg>
              </div>
              <input
                type="text"
                id="simple-search"
                bind:value={searchTerm}
                class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-primary-500 focus:border-primary-500 block w-full pl-10 p-2 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-primary-500 dark:focus:border-primary-500"
                placeholder="Search"
              />
            </div>
          </form>
        </div>
        <div class="w-full md:w-auto flex flex-col md:flex-row space-y-2 md:space-y-0 items-stretch md:items-center justify-end md:space-x-3 flex-shrink-0">
          <button
            type="button"
            class="flex items-center justify-center text-white bg-primary-700 hover:bg-primary-800 focus:ring-4 focus:ring-primary-300 font-medium rounded-lg text-sm px-4 py-2 dark:bg-primary-600 dark:hover:bg-primary-700 focus:outline-none dark:focus:ring-primary-800"
          >
            <svg class="h-3.5 w-3.5 mr-2" fill="currentColor" viewBox="0 0 20 20">
              <path clip-rule="evenodd" fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" />
            </svg>
            Add product
          </button>
        </div>
      </div>

      <!-- Tabel Produk -->
      <div class="overflow-x-auto">
        <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
          <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
              <th scope="col" class="px-4 py-3">Product name</th>
              <th scope="col" class="px-4 py-3">Category</th>
              <th scope="col" class="px-4 py-3">Brand</th>
              <th scope="col" class="px-4 py-3">Description</th>
              <th scope="col" class="px-4 py-3">Price</th>
              <th scope="col" class="px-4 py-3">
                <span class="sr-only">Actions</span>
              </th>
            </tr>
          </thead>
          <tbody>
            {#each filteredProducts as product (product.id)}
  <tr class="border-b dark:border-gray-700">
    <td class="px-4 py-3 font-medium text-gray-900 whitespace-nowrap dark:text-white">{product.name}</td>
    <td class="px-4 py-3">{product.category}</td>
    <td class="px-4 py-3">{product.brand}</td>
    <td class="px-4 py-3">{product.description}</td>
    <td class="px-4 py-3">{product.price}</td>
    <td class="px-4 py-3 flex items-center justify-end">
      <button
      on:click={() => toggleDropdown(`dropdown-${product.id}`)}
      aria-label="Toggle dropdown menu"
      class="inline-flex items-center p-0.5 text-sm font-medium text-center text-gray-500 hover:text-gray-800 rounded-lg focus:outline-none dark:text-gray-400 dark:hover:text-gray-100"
    >
      <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
        <path d="M6 10a2 2 0 11-4 0 2 2 0 014 0zM12 10a2 2 0 11-4 0 2 2 0 014 0zM16 12a2 2 0 100-4 2 2 0 000 4z" />
      </svg>
    </button>
      <!-- Dropdown Menu -->
      <div id={`dropdown-${product.id}`} class="dropdown hidden z-10 w-44 bg-white rounded divide-y divide-gray-100 shadow dark:bg-gray-700 dark:divide-gray-600">
        <ul class="py-1 text-sm text-gray-700 dark:text-gray-200">
          <li>
            <a href="/" class="block py-2 px-4 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Show</a>
          </li>
          <li>
            <a href="/" class="block py-2 px-4 hover:bg-gray-100 dark:hover:bg-gray-600 dark:hover:text-white">Edit</a>
          </li>
        </ul>
        <div class="py-1">
          <a href="/" class="block py-2 px-4 text-sm text-gray-700 hover:bg-gray-100 dark:hover:bg-gray-600 dark:text-gray-200 dark:hover:text-white">Delete</a>
        </div>
      </div>
    </td>
  </tr>
{/each} <!-- Pastikan ini ada -->
          </tbody>
        </table>
      </div>

      <!-- Pagination -->
      <nav class="flex flex-col md:flex-row justify-between items-start md:items-center space-y-3 md:space-y-0 p-4">
        <span class="text-sm font-normal text-gray-500 dark:text-gray-400">
          Showing <span class="font-semibold text-gray-900 dark:text-white">1-10</span> of <span class="font-semibold text-gray-900 dark:text-white">1000</span>
        </span>
        <ul class="inline-flex items-stretch -space-x-px">
          <li>
            <a href="/" class="flex items-center justify-center h-full py-1.5 px-3 ml-0 text-gray-500 bg-white rounded-l-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
              <span class="sr-only">Previous</span>
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M12.707 5.293a1 1 0 010 1.414L9.414 10l3.293 3.293a1 1 0 01-1.414 1.414l-4-4a1 1 0 010-1.414l4-4a1 1 0 011.414 0z" clip-rule="evenodd" />
              </svg>
            </a>
          </li>
          <li>
            <a href="/" class="flex items-center justify-center text-sm py-2 px-3 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">1</a>
          </li>
          <li>
            <a href="/" class="flex items-center justify-center text-sm py-2 px-3 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">2</a>
          </li>
          <li>
            <a href="/" aria-current="page" class="flex items-center justify-center text-sm z-10 py-2 px-3 leading-tight text-primary-600 bg-primary-50 border border-primary-300 hover:bg-primary-100 hover:text-primary-700 dark:border-gray-700 dark:bg-gray-700 dark:text-white">3</a>
          </li>
          <li>
            <a href="/" class="flex items-center justify-center text-sm py-2 px-3 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">...</a>
          </li>
          <li>
            <a href="/" class="flex items-center justify-center text-sm py-2 px-3 leading-tight text-gray-500 bg-white border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">100</a>
          </li>
          <li>
            <a href="/" class="flex items-center justify-center h-full py-1.5 px-3 leading-tight text-gray-500 bg-white rounded-r-lg border border-gray-300 hover:bg-gray-100 hover:text-gray-700 dark:bg-gray-800 dark:border-gray-700 dark:text-gray-400 dark:hover:bg-gray-700 dark:hover:text-white">
              <span class="sr-only">Next</span>
              <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20">
                <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
              </svg>
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</section>