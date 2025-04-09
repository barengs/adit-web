<script>
  import { writable } from 'svelte/store';

  export const biodata = writable({
      name: "wahyudi ken",
      age: 25,
      prodi: "Teknik Informatika",
      fakultas: "Fakultas Teknik",
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
      accounts: [
          { username: "johndoe", email: "johndoe@example.com", role: "Admin" },
          { username: "janedoe", email: "janedoe@example.com", role: "User" },
          { username: "user123", email: "user123@example.com", role: "User" }
      ]
  });
</script>

<div class="w-full max-w-3xl mx-auto p-6 bg-white shadow-lg rounded-lg">
  <h2 class="text-2xl font-semibold text-gray-800 text-center">Biodata Diri</h2>

  {#if $biodata}
      
      <div class="grid grid-cols-2 gap-6 mt-6">
          <div class="p-4 border rounded-lg">
              <h3 class="text-lg font-semibold text-gray-700">Informasi Pribadi</h3>
              <p class="text-gray-600"><strong>Nama:</strong> {$biodata.name}</p>
              <p class="text-gray-600"><strong>Usia:</strong> {$biodata.age} tahun</p>
              <p class="text-gray-600"><strong>Program Studi:</strong> {$biodata.prodi}</p>
              <p class="text-gray-600"><strong>Fakultas:</strong> {$biodata.fakultas}</p>
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

      
      <h2 class="text-xl font-semibold text-gray-800 mt-8">Akun Pengguna</h2>
      <div class="mt-4 p-4 border rounded-lg">
          <table class="w-full text-left border-collapse">
              <thead>
                  <tr class="bg-gray-200">
                      <th class="p-2 border">Username</th>
                      <th class="p-2 border">Email</th>
                      <th class="p-2 border">Role</th>
                  </tr>
              </thead>
              <tbody>
                  {#each $biodata.accounts as acc}
                      <tr class="hover:bg-gray-100 transition">
                          <td class="p-2 border">{acc.username}</td>
                          <td class="p-2 border">{acc.email}</td>
                          <td class="p-2 border">{acc.role}</td>
                      </tr>
                  {/each}
              </tbody>
          </table>
      </div>
  {/if}
</div>

<style>
  td, th {
      text-align: left;
  }
</style>
