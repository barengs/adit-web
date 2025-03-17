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
    accounts: [
      { username: "johndoe", email: "johndoe@example.com", role: "Admin" },
      { username: "janedoe", email: "janedoe@example.com", role: "User" },
      { username: "user123", email: "user123@example.com", role: "User" }
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
    </div>
    
    <h2 class="text-xl font-semibold mt-6">Akun Pengguna</h2>
    <table class="w-full text-left border-collapse border border-gray-300 mt-4">
      <thead>
        <tr>
          <th class="p-2 border border-gray-300">Username</th>
          <th class="p-2 border border-gray-300">Email</th>
          <th class="p-2 border border-gray-300">Role</th>
        </tr>
      </thead>
      <tbody>
        {#each $biodata.accounts as acc}
          <tr>
            <td class="p-2 border border-gray-300 font-semibold">{acc.username}</td>
            <td class="p-2 border border-gray-300">{acc.email}</td>
            <td class="p-2 border border-gray-300">{acc.role}</td>
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
