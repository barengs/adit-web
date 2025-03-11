<script>
    import { writable } from 'svelte/store';
  
    
    export const biodata = writable({
      name: "John Doe",
      age: 25,
       prodi: "teknik informatika",
      photo: "/path/to/photo.jpg",
      email: "johndoe@example.com",
      phone: "+62 812-3456-7890",
     
    });
  </script>
  
  <div class="w-[70vh] mx-auto p-6 bg-white shadow-md rounded-lg">
    <h2 class="text-xl font-semibold mb-4">Biodata Diri</h2>
  
   
    {#if $biodata}
      <div class="flex flex-col items-center">
        <img src="/brosurdua.jpg" alt="brosur" class="w-40 h-40 rounded-full">

  
        <table class="w-full text-left border-collapse">
          <tbody>
            <tr>
              <td class="font-semibold">Nama</td>
              <td>: {$biodata.name}</td>
            </tr>
            <tr>
              <td class="font-semibold">Usia</td>
              <td>: {$biodata.age} tahun</td>
            </tr>
            <tr>
              <td class="font-semibold">Prodi</td>
              <td>: {$biodata.prodi}</td>
            </tr>
            <tr>
              <td class="font-semibold">Email</td>
              <td>: {$biodata.email}</td>
            </tr>
            <tr>
              <td class="font-semibold">Telepon</td>
              <td>: {$biodata.phone}</td>
            </tr>
          </tbody>
        </table>
      </div>
    {/if}
  </div>
  
  <style>
    table td {
      padding: 8px;
    }
  </style>
  