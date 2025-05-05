<script>
import { Button, Modal } from 'flowbite-svelte';
let defaultModal = false;
import { createEventDispatcher } from 'svelte';
  
  let step = 1;
  const dispatch = createEventDispatcher();

  function next() {
    if (step < 5) step++;
  }

  function prev() {
    if (step > 1) step--;
  }

  function finish() {
    dispatch('finish');
    defaultModal = false;
  }
</script>
  
  <Button on:click={() => (defaultModal = true)}>Default modal</Button>
  <Modal title="Terms of Service" bind:open={defaultModal} placement='top-center'>
   
    <div class="max-w-2xl mx-auto mt-10 p-6 bg-white ">
        
        <div class="flex justify-between mb-8">
            {#each Array(5) as _, i}
              <div class="w-full flex items-center">
                <div class={`flex items-center justify-center w-8 h-8 rounded-full ${step >= i + 1 ? 'bg-blue-500 text-white' : 'bg-gray-300'}`}>
                  {i + 1}
                </div>
                {#if i < 4}
                  <div class="flex-1 h-1 bg-gray-300"></div>
                {/if}
              </div>
            {/each}
          </div>
      
        
        {#if step === 1}
          <div>
            <h2 class="text-xl font-semibold mb-4">Step 1: Data Pribadi</h2>
            <div class="space-y-4">
              <input type="text" placeholder="Nama Lengkap" class="w-full p-2 border rounded-md" />
              <input type="email" placeholder="Email" class="w-full p-2 border rounded-md" />
            </div>
          </div>
        {:else if step === 2}
          <div>
            <h2 class="text-xl font-semibold mb-4">Step 2: Alamat</h2>
            <div class="space-y-4">
              <input type="text" placeholder="Alamat Lengkap" class="w-full p-2 border rounded-md" />
              <input type="text" placeholder="Kota" class="w-full p-2 border rounded-md" />
            </div>
          </div>
        {:else if step === 3}
          <div>
            <h2 class="text-xl font-semibold mb-4">Step 3: Konfirmasi</h2>
            <p class="text-gray-600 mb-6">Periksa kembali data Anda sebelum submit.</p>
          </div>
          {:else if step === 4}
          <div>
            <h2 class="text-xl font-semibold mb-4">Step 4: Metode Pembayaran</h2>
            <div class="space-y-4">
              <select class="w-full p-2 border rounded-md">
                <option>Transfer Bank</option>
                <option>COD</option>
                <option>E-Wallet</option>
              </select>
            </div>
          </div>
        {:else if step === 5}
          <div>
            <h2 class="text-xl font-semibold mb-4">Step 5: Selesai</h2>
            <p class="text-gray-600 mb-6">Data Anda sudah lengkap! Klik selesai untuk mengirim.</p>
          </div>
        {/if}
      
        
        <div class="flex justify-between mt-8">
          {#if step > 1}
            <button on:click={prev} class="px-4 py-2 bg-gray-300 hover:bg-gray-400 text-black rounded-md">
              Kembali
            </button>
          {/if}
      
          {#if step < 5}
          <button on:click={next} class="ml-auto px-4 py-2 bg-blue-500 hover:bg-blue-600 text-white rounded-md">
            Selanjutnya
          </button>
        {:else}
          <button on:click={finish} class="ml-auto px-4 py-2 bg-green-500 hover:bg-green-600 text-white rounded-md">
            Selesai
          </button>
        {/if}
        </div>
      </div>
      
    
   
  </Modal>