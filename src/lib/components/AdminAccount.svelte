<script>
  
  import { Button } from 'flowbite-svelte';
  import ModalAdmin from './ModalAdmin.svelte';
  

</script>



<div class=" w-[1050px] mx-auto bg-white rounded-lg shadow-md overflow-hidden p-6 space-y-6">
    
  
  
    <div class="flex flex-col items-center space-y-3">
      <div class="w-24 h-24 bg-gray-300 rounded-full"></div>
      <div class="flex gap-2">
        <h2 class="text-xl font-semibold text-gray-800">Nama Lengkap</h2>
          <ModalAdmin/>
      </div>
      <p class="text-gray-600">Program Studi - Fakultas</p>
    </div>
  

   
    
   
    
    

    <div class="space-y-2">
      <h3 class="text-lg font-semibold text-gray-700">Informasi Kontak</h3>
      <p class="text-gray-700"><strong>Email :</strong> contoh@email.com</p>
      <p class="text-gray-700"><strong>Telepon :</strong> 08123456789</p>
    </div>
  
   
    <div class="space-y-2">
      <h3 class="text-lg font-semibold text-gray-700">Alamat :</h3>
      <p class="text-gray-700">Provinsi, Kota, Kecamatan</p>
    </div>
  </div>
  
  <style>
    div {
      transition: all 0.3s ease-in-out;
    }
  </style>
  