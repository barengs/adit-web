<script>
  import { Button, Modal, Label, Input } from "flowbite-svelte";
  let defaultModal = false;

  let step = 1;

  let formData = {
    name: "",
    email: "",
    address: "",
    city: "",
  };

  function nextStep() {
    if (step < 3) step += 1;
  }

  function prevStep() {
    if (step > 1) step -= 1;
  }

  function submitForm() {
    console.log("Form Data:", formData);
    defaultModal = false;
    step = 1;
  }
</script>

<Button on:click={() => (defaultModal = true)} class='bg-green-700'>lengkapi pendaftaran</Button>

<Modal title="Form Wizard" bind:open={defaultModal} autoclose={false} placement="top-center">

  <div class="flex justify-center gap-4 mb-6">
  {#each [1, 2, 3] as i}
    <div class="flex flex-col items-center">
      <div class={`w-8 h-8 rounded-full flex items-center justify-center font-semibold
        ${i === step ? 'bg-blue-600 text-white' : 'bg-gray-200 text-gray-600'}`}>
        {i}
      </div>
      <p class="text-sm mt-1 text-gray-700">Step {i}</p>
    </div>
  {/each}
</div>

  {#if step === 1}
    <div class="space-y-4">
      <h3 class="text-lg font-semibold">Step 1: data diri</h3>
      <div>
        <Label for="name">Nama</Label>
        <Input id="name" bind:value={formData.name} placeholder="Your name" />
      </div>
      <div>
        <Label for="email">Email</Label>
        <Input id="email" bind:value={formData.email} placeholder="you@example.com" type="email" />
      </div>
    </div>
  {:else if step === 2}
    <div class="space-y-4">
      <h3 class="text-lg font-semibold">Step 2: alamat</h3>
      <div>
        <Label for="address">Address</Label>
        <Input id="address" bind:value={formData.address} placeholder="123 Main St" />
      </div>
      <div>
        <Label for="city">City</Label>
        <Input id="city" bind:value={formData.city} placeholder="Your city" />
      </div>
    </div>
  {:else if step === 3}
    <div class="space-y-4">
      <h3 class="text-lg font-semibold">Step 3: Confirm</h3>
      <p><strong>Name:</strong> {formData.name}</p>
      <p><strong>Email:</strong> {formData.email}</p>
      <p><strong>Address:</strong> {formData.address}</p>
      <p><strong>City:</strong> {formData.city}</p>
    </div>
  {/if}

  <div class="flex justify-between mt-6">
    {#if step > 1}
      <Button on:click={prevStep}>Back</Button>
    {/if}
    {#if step < 3}
      <Button on:click={nextStep}>Next</Button>
    {:else}
      <Button on:click={submitForm}>Submit</Button>
    {/if}
  </div>
</Modal>
