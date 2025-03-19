<script>
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';
  
  let isRegister = writable(false);
  let username = '';
  let password = '';
  let role = 'user';

  async function handleSubmit() {
    if ($isRegister) {
      // Proses registrasi (simulasi penyimpanan ke db.json)
      console.log('Registering:', { username, password, role });
    } else {
      // Proses login (simulasi validasi dari db.json)
      console.log('Logging in:', { username, password });

      if (role === 'admin') {
        goto('/dataakun'); // Admin diarahkan ke /dataakun (bisa ditambahkan redirect lain)
      } else {
        goto('/home'); // User biasa diarahkan ke /home
      }
    }
  }
</script>

<div class="max-w-md mx-auto p-6 bg-white shadow-md rounded-lg">
  <h2 class="text-xl font-semibold mb-4">{$isRegister ? 'Register' : 'Login'}</h2>
  
  <form on:submit|preventDefault={handleSubmit}>
    <label class="block mb-2" for="username">Username</label>
    <input id="username" type="text" bind:value={username} class="w-full p-2 border rounded mb-4" required />
    
    <label class="block mb-2" for="password">Password</label>
    <input id="password" type="password" bind:value={password} class="w-full p-2 border rounded mb-4" required />
    
    {#if $isRegister}
      <label class="block mb-2" for="role">Role</label>
      <select id="role" bind:value={role} class="w-full p-2 border rounded mb-4">
        <option value="user">User</option>
        <option value="admin">Admin</option>
      </select>
    {/if}
    
    <button type="submit" class="w-full p-2 bg-blue-500 text-white rounded">
      {$isRegister ? 'Register' : 'Login'}
    </button>
  </form>
  
  <p class="mt-4 text-center">
    {$isRegister ? 'Sudah punya akun?' : 'Belum punya akun?'}
    <button type="button" on:click={() => isRegister.set(!$isRegister)} class="text-blue-500 underline">
      {$isRegister ? 'Login di sini' : 'Daftar di sini'}
    </button>
  </p>
  
  
</div>
