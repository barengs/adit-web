<script>
    import { writable } from 'svelte/store';
  
    export const biodata = writable({
      name: "John Doe",
      age: 25,
      prodi: "teknik informatika",
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
  
<div class="w-full mx-auto p-6 bg-white shadow-md rounded-lg">
    <h2 class="text-xl font-semibold mb-4">Biodata Diri</h2>
  
    {#if $biodata}
      <div class="grid grid-cols-2 gap-4">
        <table class="w-full text-left border-collapse border border-gray-300">
          <tbody>
            <tr><td class="p-2 border border-gray-300 font-semibold">Nama</td><td class="p-2 border border-gray-300">{$biodata.name}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Usia</td><td class="p-2 border border-gray-300">{$biodata.age} tahun</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Prodi</td><td class="p-2 border border-gray-300">{$biodata.prodi}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Email</td><td class="p-2 border border-gray-300">{$biodata.email}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Telepon</td><td class="p-2 border border-gray-300">{$biodata.phone}</td></tr>
          </tbody>
        </table>
        <table class="w-full text-left border-collapse border border-gray-300">
          <tbody>
            <tr><td class="p-2 border border-gray-300 font-semibold">Provinsi</td><td class="p-2 border border-gray-300">{$biodata.address.provinsi}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Kota/Kabupaten</td><td class="p-2 border border-gray-300">{$biodata.address.kota}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Kecamatan</td><td class="p-2 border border-gray-300">{$biodata.address.kecamatan}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Kelurahan</td><td class="p-2 border border-gray-300">{$biodata.address.kelurahan}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">Dusun</td><td class="p-2 border border-gray-300">{$biodata.address.dusun}</td></tr>
            <tr><td class="p-2 border border-gray-300 font-semibold">RT/RW</td><td class="p-2 border border-gray-300">{$biodata.address.rt} / {$biodata.address.rw}</td></tr>
          </tbody>
        </table>
      </div>
    {/if}
</div>

<style>
    td {
        text-align: left;
    }
</style>
