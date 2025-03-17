<script>
  import { writable } from 'svelte/store';

  export const biodata = writable({
    name: "John Doe",
    age: 25,
    prodi: "Teknik Informatika",
    fakultas: "Fakultas Teknik",
    email: "johndoe@example.com",
    phone: "+62 812-3456-7890",
    photo: "/brosurdua.jpg",
    status_pmb: "Diterima",
    address: {
      provinsi: "Jawa Tengah",
      kota: "Semarang",
      kecamatan: "Tembalang",
      kelurahan: "Meteseh",
      dusun: "Dusun Krajan",
      rt: "04",
      rw: "02"
    },
    orang_tua: {
      ayah: { nama: "Budi Santoso", pekerjaan: "PNS" },
      ibu: { nama: "Siti Aminah", pekerjaan: "Ibu Rumah Tangga" }
    },
    pendidikan: {
      sekolah_asal: "SMA Negeri 1 Semarang",
      jurusan: "IPA",
      tahun_lulus: 2019
    }
  });

  let activeTab = 'status_pmb'; 
</script>

<div class="w-full mx-auto p-6 bg-white shadow-md rounded-lg">
  <h2 class="text-2xl font-bold mb-6 text-center">Biodata Diri</h2>

  
  <div class="border-b border-gray-200 flex justify-center space-x-4">
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
    {#if activeTab === 'status_pmb'}
      <h3 class="text-lg font-semibold mb-2">Status Penerimaan Mahasiswa Baru</h3>
      <p class="text-gray-700"><strong>Status:</strong> {$biodata.status_pmb}</p>

    {:else if activeTab === 'alamat'}
      <h3 class="text-lg font-semibold mb-2">Alamat Lengkap</h3>
      <p class="text-gray-700"><strong>Provinsi:</strong> {$biodata.address.provinsi}</p>
      <p class="text-gray-700"><strong>Kota:</strong> {$biodata.address.kota}</p>
      <p class="text-gray-700"><strong>Kecamatan:</strong> {$biodata.address.kecamatan}</p>
      <p class="text-gray-700"><strong>Kelurahan:</strong> {$biodata.address.kelurahan}</p>
      <p class="text-gray-700"><strong>Dusun:</strong> {$biodata.address.dusun}</p>
      <p class="text-gray-700"><strong>RT/RW:</strong> {$biodata.address.rt}/{$biodata.address.rw}</p>

    {:else if activeTab === 'data_ortu'}
      <h3 class="text-lg font-semibold mb-2">Data Orang Tua</h3>
      <p class="text-gray-700"><strong>Nama Ayah:</strong> {$biodata.orang_tua.ayah.nama}</p>
      <p class="text-gray-700"><strong>Pekerjaan Ayah:</strong> {$biodata.orang_tua.ayah.pekerjaan}</p>
      <p class="text-gray-700"><strong>Nama Ibu:</strong> {$biodata.orang_tua.ibu.nama}</p>
      <p class="text-gray-700"><strong>Pekerjaan Ibu:</strong> {$biodata.orang_tua.ibu.pekerjaan}</p>

    {:else if activeTab === 'data_pendidikan'}
      <h3 class="text-lg font-semibold mb-2">Data Pendidikan</h3>
      <p class="text-gray-700"><strong>Sekolah Asal:</strong> {$biodata.pendidikan.sekolah_asal}</p>
      <p class="text-gray-700"><strong>Jurusan:</strong> {$biodata.pendidikan.jurusan}</p>
      <p class="text-gray-700"><strong>Tahun Lulus:</strong> {$biodata.pendidikan.tahun_lulus}</p>
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
