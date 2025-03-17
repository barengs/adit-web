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
      },
      parents: {
        ayah: {
          name: "Budi Santoso",
          address: "Jalan Merdeka No.10, Semarang",
          pekerjaan: "Pegawai Negeri",
          phone: "+62 812-1111-2222",
          golDarah: "A"
        },
        ibu: {
          name: "Siti Aminah",
          address: "Jalan Merdeka No.10, Semarang",
          pekerjaan: "Ibu Rumah Tangga",
          phone: "+62 812-3333-4444",
          golDarah: "B"
        },
        wali: {
          name: "Haryanto",
          address: "Jalan Sudirman No.5, Semarang",
          pekerjaan: "Wiraswasta",
          phone: "+62 812-5555-6666",
          golDarah: "O"
        }
      },
      education: [
        { level: "SD", name: "SD Negeri 1 Semarang", year: "2005 - 2011" },
        { level: "SMP", name: "SMP Negeri 5 Semarang", year: "2011 - 2014" },
        { level: "SMA", name: "SMA Negeri 3 Semarang", year: "2014 - 2017" }
      ]
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
      
      <h2 class="text-xl font-semibold mt-6">Riwayat Pendidikan</h2>
      <table class="w-full text-left border-collapse border border-gray-300 mt-4">
        <thead>
          <tr>
            <th class="p-2 border border-gray-300">Jenjang</th>
            <th class="p-2 border border-gray-300">Nama Sekolah</th>
            <th class="p-2 border border-gray-300">Tahun</th>
          </tr>
        </thead>
        <tbody>
          {#each $biodata.education as edu}
            <tr>
              <td class="p-2 border border-gray-300 font-semibold">{edu.level}</td>
              <td class="p-2 border border-gray-300">{edu.name}</td>
              <td class="p-2 border border-gray-300">{edu.year}</td>
            </tr>
          {/each}
        </tbody>
      </table>
    {/if}
</div>

<style>
    td {
        text-align: left;
    }
</style>
