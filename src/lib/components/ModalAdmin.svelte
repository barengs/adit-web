<script lang="ts">
    
    import { Button, Modal } from "flowbite-svelte";
    let defaultModal = false;
    let firstname = '';
    let lastname = '';
	let email = '';
	let password = '';
	let password2 = '';

	let errors = {
		firstname: '',
		lastname: '',
		email: '',
		password: '',
		password2: ''
	};

	const isValidEmail = (email: String) => {
		const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
		return re.test(String(email).toLowerCase());
	};

	const validateInputs = () => {
		errors = {
			firstname: '',
			lastname: '',
			email: '',
			password: '',
			password2: ''
		};

		if (firstname.trim() === '') {
			errors.firstname = 'Username is required';
		}
		if (lastname.trim() === '') {
			errors.lastname = 'Username is required';
		}

		if (email.trim() === '') {
			errors.email = 'Email is required';
		} else if (!isValidEmail(email)) {
			errors.email = 'Provide a valid email address';
		}

		if (password.trim() === '') {
			errors.password = 'Password is required';
		} else if (password.length < 8) {
			errors.password = 'Password must be at least 8 characters';
		}

		if (password2.trim() === '') {
			errors.password2 = 'Please confirm your password';
		} else if (password2 !== password) {
			errors.password2 = "Passwords don't match";
		}
	};

	const handleSubmit = (e: Event) => {
		e.preventDefault();
		validateInputs();
		
	};
  

  </script>
  
  <Button 
  class=" bg-blue-200 p-2 rounded-full text-gray-500 hover:bg-gray-200"
  on:click={() => (defaultModal = true)}
>
  
  <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15.232 5.232l3.536 3.536M9 11l3.536-3.536a2 2 0 012.828 0l3.536 3.536a2 2 0 010 2.828L11 21H7v-4L15.232 5.232z" />
  </svg>
</Button>
  <Modal title="" bind:open={defaultModal} placement='top-center'>
    <div class=" flex  font-poppins">
        <form on:submit|preventDefault={handleSubmit} class="w-80 bg-white p-6 rounded-md text-sm">
            <h1 class=" text-[#0f2027] text-xl mb-6">Data Diri</h1>
    <div class="flex gap-6"> 
            <div class="flex flex-col mb-4">
                <label for="firstname" class="mb-1">nama depan</label>
                <input
                    id="firstname"
                    bind:value={firstname}
                    type="text"
                    class="border-2 rounded-md p-2 focus:outline-none {errors.firstname ? 'border-red-500' : 'border-gray-200'}"
                />
                <p class="text-red-500 text-xs h-4">{errors.firstname}</p>
            </div>
    
            <div class="flex flex-col mb-4">
                <label for="lastname" class="mb-1">nama belakang</label>
                <input
                    id="lastname"
                    bind:value={lastname}
                    type="text"
                    class="border-2 rounded-md p-2 focus:outline-none {errors.lastname ? 'border-red-500' : 'border-gray-200'}"
                />
                <p class="text-red-500 text-xs h-4">{errors.lastname}</p>
            </div>
        </div>
            <div class="flex flex-col mb-4">
                <label for="email" class="mb-1">Email</label>
                <input
                    id="email"
                    bind:value={email}
                    type="text"
                    class="border-2 rounded-md p-2 focus:outline-none {errors.email ? 'border-red-500' : 'border-gray-200'}"
                />
                <p class="text-red-500 text-xs h-4">{errors.email}</p>
            </div>
    
            <div class="flex flex-col mb-4">
                <label for="password" class="mb-1">Password</label>
                <input
                    id="password"
                    bind:value={password}
                    type="password"
                    class="border-2 rounded-md p-2 focus:outline-none {errors.password ? 'border-red-500' : 'border-gray-200'}"
                />
                <p class="text-red-500 text-xs h-4">{errors.password}</p>
            </div>
    
            <div class="flex flex-col mb-4">
                <label for="password2" class="mb-1">Password again</label>
                <input
                    id="password2"
                    bind:value={password2}
                    type="password"
                    class="border-2 rounded-md p-2 focus:outline-none {errors.password2 ? 'border-red-500' : 'border-gray-200'}"
                />
                <p class="text-red-500 text-xs h-4">{errors.password2}</p>
            </div>
    
            <button type="submit" class="w-full bg-blue-700 text-white py-2 rounded-md mt-2 hover:bg-blue-800 transition">
                simpan
            </button>
        </form>
    </div>
    
    
    
</Modal>