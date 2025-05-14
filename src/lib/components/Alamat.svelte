<script>
  import { writable } from 'svelte/store';

  export const biodata = writable({
    name: "John Doe",
    age: 25,
    prodi: "Teknik Informatika",
    email: "johndoe@example.com",
    phone: "+62 812-3456-7890",
    address: {
      provinsi: "Jawa Tengah",
      kota: "Semarang",
      kecamatan: "Tembalang",
      kelurahan: "Meteseh",
      dusun: "Dusun Krajan",
      rt: "04",
      rw: "02"
    }
  });
</script>

<div class="w-full max-w-3xl  p-6 bg-white shadow-md rounded-lg">

  {#if $biodata}
    <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
      
      <!-- Card Data Diri -->
      <div class="bg-gray-100 p-6 rounded-lg shadow">
        <p class="mb-2"><strong>Nama:</strong> {$biodata.name}</p>
        <p class="mb-2"><strong>Usia:</strong> {$biodata.age} tahun</p>
        <p class="mb-2"><strong>Prodi:</strong> {$biodata.prodi}</p>
        <p class="mb-2"><strong>Email:</strong> {$biodata.email}</p>
        <p class="mb-2"><strong>Telepon:</strong> {$biodata.phone}</p>
      </div>

      <!-- Card Alamat -->
      <div class="bg-gray-100 p-6 rounded-lg shadow">
        <p class="mb-2"><strong>Provinsi:</strong> {$biodata.address.provinsi}</p>
        <p class="mb-2"><strong>Kota/Kabupaten:</strong> {$biodata.address.kota}</p>
        <p class="mb-2"><strong>Kecamatan:</strong> {$biodata.address.kecamatan}</p>
        <p class="mb-2"><strong>Kelurahan:</strong> {$biodata.address.kelurahan}</p>
        <p class="mb-2"><strong>Dusun:</strong> {$biodata.address.dusun}</p>
        <p class="mb-2"><strong>RT/RW:</strong> {$biodata.address.rt} / {$biodata.address.rw}</p>
      </div>

    </div>
  {/if}
</div>

<style>
div {
  transition: all 0.3s ease-in-out;
}
</style>
