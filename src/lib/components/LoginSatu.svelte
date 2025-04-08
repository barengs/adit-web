<script lang="ts">
  import { writable } from 'svelte/store';
  import { goto } from '$app/navigation';

  const isRegister = writable(false);

  let username = '';
  let password = '';
  let role: 'user' | 'admin' = 'user';

  interface User {
    username: string;
    password: string;
    role: 'user' | 'admin';
  }

  async function handleSubmit() {
    if ($isRegister) {
      // === REGISTRASI ===
      const newUser: User = { username, password, role };

      try {
        const res = await fetch('http://localhost:3000/users', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify(newUser)
        });

        if (res.ok) {
          alert('Registrasi berhasil! Silakan login.');
          isRegister.set(false);
        } else {
          alert('Registrasi gagal.');
        }
      } catch (err) {
        console.error('Error saat registrasi:', err);
        alert('Terjadi kesalahan saat registrasi.');
      }

    } else {
      // === LOGIN ===
      try {
        const res = await fetch('http://localhost:3000/users');
        if (!res.ok) throw new Error('Gagal mengambil data users');

        const users = (await res.json()) as User[];

        const found = users.find(
          (u) => u.username === username && u.password === password
        );

        if (found) {
          // Simpan info login
          localStorage.setItem('username', found.username);
          localStorage.setItem('role', found.role);

          // Arahkan sesuai role
          if (found.role === 'admin') {
            goto('/dataakun');
          } else {
            goto('/home');
          }
        } else {
          alert('Username atau password salah!');
        }
      } catch (err) {
        console.error('Error saat login:', err);
        alert('Terjadi kesalahan saat login.');
      }
    }
  }
</script>

<!-- UI -->
<div class="max-w-md mx-auto p-6 bg-white shadow-md rounded-lg mt-10">
  <h2 class="text-2xl font-bold text-center mb-4">{$isRegister ? 'Register' : 'Login'}</h2>

  <form on:submit|preventDefault={handleSubmit}>
    <label for="username" class="block mb-1">Username</label>
    <input id="username" bind:value={username} class="w-full p-2 border rounded mb-4" required />

    <label for="password" class="block mb-1">Password</label>
    <input id="password" type="password" bind:value={password} class="w-full p-2 border rounded mb-4" required />

    {#if $isRegister}
      <label for="role" class="block mb-1">Role</label>
      <select id="role" bind:value={role} class="w-full p-2 border rounded mb-4">
        <option value="user">User</option>
        <option value="admin">Admin</option>
      </select>
    {/if}

    <button type="submit" class="w-full bg-blue-600 text-white py-2 rounded hover:bg-blue-700">
      {$isRegister ? 'Daftar' : 'Login'}
    </button>
  </form>

  <p class="mt-4 text-center text-sm">
    {$isRegister ? 'Sudah punya akun?' : 'Belum punya akun?'}
    <button
      type="button"
      on:click={() => isRegister.set(!$isRegister)}
      class="text-blue-600 font-semibold hover:underline"
    >
      {$isRegister ? 'Login di sini' : 'Daftar di sini'}
    </button>
  </p>
</div>
