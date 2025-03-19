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
    },
    parents: {
      ayah: { name: "Budi Santoso", pekerjaan: "Pegawai Negeri", phone: "+62 812-1111-2222", golDarah: "A" },
      ibu: { name: "Siti Aminah", pekerjaan: "Ibu Rumah Tangga", phone: "+62 812-3333-4444", golDarah: "B" },
      wali: { name: "Haryanto", pekerjaan: "Wiraswasta", phone: "+62 812-5555-6666", golDarah: "O" }
    },
    education: [
      { level: "SD", name: "SD Negeri 1 Semarang", year: "2005 - 2011" },
      { level: "SMP", name: "SMP Negeri 5 Semarang", year: "2011 - 2014" },
      { level: "SMA", name: "SMA Negeri 3 Semarang", year: "2014 - 2017" }
    ]
  });
</script>

<div class="w-full max-w-3xl mx-auto p-6 bg-white shadow-md rounded-lg">
<h2 class="text-2xl font-semibold text-gray-800 text-center">Biodata Diri</h2>

<!-- Biodata -->
<div class="grid grid-cols-2 gap-6 mt-6">
  <div class="p-4 border rounded-lg">
    <h3 class="text-lg font-semibold text-gray-700">Informasi Pribadi</h3>
    <p class="text-gray-600"><strong>Nama:</strong> {$biodata.name}</p>
    <p class="text-gray-600"><strong>Usia:</strong> {$biodata.age} tahun</p>
    <p class="text-gray-600"><strong>Program Studi:</strong> {$biodata.prodi}</p>
    <p class="text-gray-600"><strong>Email:</strong> {$biodata.email}</p>
    <p class="text-gray-600"><strong>Telepon:</strong> {$biodata.phone}</p>
  </div>

  <div class="p-4 border rounded-lg">
    <h3 class="text-lg font-semibold text-gray-700">Alamat</h3>
    <p class="text-gray-600"><strong>Provinsi:</strong> {$biodata.address.provinsi}</p>
    <p class="text-gray-600"><strong>Kota:</strong> {$biodata.address.kota}</p>
    <p class="text-gray-600"><strong>Kecamatan:</strong> {$biodata.address.kecamatan}</p>
    <p class="text-gray-600"><strong>Kelurahan:</strong> {$biodata.address.kelurahan}</p>
    <p class="text-gray-600"><strong>Dusun:</strong> {$biodata.address.dusun}</p>
    <p class="text-gray-600"><strong>RT/RW:</strong> {$biodata.address.rt} / {$biodata.address.rw}</p>
  </div>
</div>

<!-- Riwayat Pendidikan -->
<h2 class="text-xl font-semibold text-gray-800 mt-8">Riwayat Pendidikan</h2>
<div class="mt-4 p-4 border rounded-lg">
  <table class="w-full text-left border-collapse">
    <thead>
      <tr class="bg-gray-200">
        <th class="p-2 border">Jenjang</th>
        <th class="p-2 border">Nama Sekolah</th>
        <th class="p-2 border">Tahun</th>
      </tr>
    </thead>
    <tbody>
      {#each $biodata.education as edu}
        <tr class="hover:bg-gray-100">
          <td class="p-2 border">{edu.level}</td>
          <td class="p-2 border">{edu.name}</td>
          <td class="p-2 border">{edu.year}</td>
        </tr>
      {/each}
    </tbody>
  </table>
</div>

<!-- Data Orang Tua & Wali -->
<h2 class="text-xl font-semibold text-gray-800 mt-8">Data Orang Tua & Wali</h2>
<div class="grid grid-cols-3 gap-6 mt-4">
  {#each Object.entries($biodata.parents) as [key, parent]}
    <div class="p-4 border rounded-lg">
      <h3 class="text-lg font-semibold text-gray-700 capitalize">{key}</h3>
      <p class="text-gray-600"><strong>Nama:</strong> {parent.name}</p>
      <p class="text-gray-600"><strong>Pekerjaan:</strong> {parent.pekerjaan}</p>
      <p class="text-gray-600"><strong>Nomor HP:</strong> {parent.phone}</p>
      <p class="text-gray-600"><strong>Golongan Darah:</strong> {parent.golDarah}</p>
    </div>
  {/each}
</div>
</div>

<style>
td, th {
  text-align: left;
}
</style>
