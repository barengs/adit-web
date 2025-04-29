<script>
  
  import { Button } from 'flowbite-svelte';
  

</script>

<div class="w-full max-w-md mx-auto bg-white rounded-lg shadow-md overflow-hidden p-6 space-y-6">
    
    <div class="flex flex-col items-center space-y-3">
      <div class="w-24 h-24 bg-gray-300 rounded-full"></div>
      <h2 class="text-xl font-semibold text-gray-800">Nama Lengkap</h2>
      <p class="text-gray-600">Program Studi - Fakultas</p>
    </div>
  

   <div class="m-[140px] [50px]">
    <Button color='purple'>edit profil</Button>
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
  