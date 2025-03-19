<script>
  
  import Alamat from './Alamat.svelte';
  import Ortu from './Ortu.svelte';
  import Pendidikan from './Pendidikan.svelte';
  import Profil from './Profil.svelte';

  

  let activeTab = 'status_pmb'; 
</script>

<div class="w-full mx-auto p-6 bg-white shadow-md rounded-lg">
  <h2 class="text-2xl font-bold mb-6 text-center">Biodata Diri</h2>

  
  <div class="border-b border-gray-200 flex justify-center space-x-4">
    
    <button 
    on:click={() => activeTab = 'Profil'}
    class="p-4 border-b-2"
    class:border-blue-600={activeTab === 'Profil'}
    class:text-blue-600={activeTab === 'Profil'}
    class:font-semibold={activeTab === 'Profil'}>
    Profil
  </button>
    
    <button 
      on:click={() => activeTab = 'status_pmb'}
      class="p-4 border-b-2"
      class:border-blue-600={activeTab === 'status_pmb'}
      class:text-blue-600={activeTab === 'status_pmb'}
      class:font-semibold={activeTab === 'status_pmb'}>
      Status PMB
    </button>

    <button 
      on:click={() => activeTab = 'alamat'}
      class="p-4 border-b-2"
      class:border-blue-600={activeTab === 'alamat'}
      class:text-blue-600={activeTab === 'alamat'}
      class:font-semibold={activeTab === 'alamat'}>
      Alamat
    </button>

    <button 
      on:click={() => activeTab = 'data_ortu'}
      class="p-4 border-b-2"
      class:border-blue-600={activeTab === 'data_ortu'}
      class:text-blue-600={activeTab === 'data_ortu'}
      class:font-semibold={activeTab === 'data_ortu'}>
      Data Orang Tua
    </button>

    <button 
      on:click={() => activeTab = 'data_pendidikan'}
      class="p-4 border-b-2"
      class:border-blue-600={activeTab === 'data_pendidikan'}
      class:text-blue-600={activeTab === 'data_pendidikan'}
      class:font-semibold={activeTab === 'data_pendidikan'}>
      Data Pendidikan
    </button>

    

  </div>

  
  <div class="mt-6">
    {#if activeTab === 'Profil'}
    <Profil/>

    {:else if activeTab === 'alamat'}
      <Alamat/>
      

    {:else if activeTab === 'data_ortu'}
      <Ortu/>
      

    {:else if activeTab === 'data_pendidikan'}
      <Pendidikan/>

    {:else if activeTab === 'status_pmb'}
    <h3 class="text-lg font-semibold mb-2">Status Penerimaan Mahasiswa Baru</h3>
    <p class="text-gray-700"><strong>Status:</strong>Diterima</p>
    
      
    {/if}
  </div>
</div>

<style>
  button {
    transition: all 0.2s;
    padding: 10px 20px;
  }
  button:hover {
    background-color: #f1f5f9;
  }
</style>
