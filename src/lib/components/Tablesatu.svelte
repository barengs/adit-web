<script lang="ts">
    import {
      Table,
      TableBody,
      TableBodyCell,
      TableBodyRow,
      TableHead,
      TableHeadCell,
      ImagePlaceholder,
      Modal
    } from 'flowbite-svelte';
    import { slide } from 'svelte/transition';
  
    // Data tabel
    const items: { name: string; color: string; type: string; price: string }[] = [
      { name: 'Apple MacBook Pro 17"', color: "Silver", type: "Laptop", price: "$2999" },
      { name: "Microsoft Surface Pro", color: "White", type: "Laptop PC", price: "$1999" },
      { name: "Magic Mouse 2", color: "Black", type: "Accessories", price: "$99" },
    ];
  
    // Menentukan tipe variabel
    let openRow: number | null = null;  
    let details: { name: string; color: string; type: string; price: string } | null = null;
    let doubleClickModal: boolean = false;
  
    // Fungsi toggleRow dengan tipe parameter eksplisit
    function toggleRow(i: number) {
      openRow = openRow === i ? null : i;
    }
  
    // Fungsi membuka modal dengan tipe parameter eksplisit
    function openModal(item: { name: string; color: string; type: string; price: string }) {
      details = item;
      doubleClickModal = true;
    }
  </script>
  
  <Table>
    <TableHead>
      <TableHeadCell>Product Name</TableHeadCell>
      <TableHeadCell>Color</TableHeadCell>
      <TableHeadCell>Category</TableHeadCell>
      <TableHeadCell>Price</TableHeadCell>
    </TableHead>
    
    <TableBody tableBodyClass="divide-y">
      {#each items as item, i}
        <TableBodyRow on:click={() => toggleRow(i)}>
          <TableBodyCell>{item.name}</TableBodyCell>
          <TableBodyCell>{item.color}</TableBodyCell>
          <TableBodyCell>{item.type}</TableBodyCell>
          <TableBodyCell>{item.price}</TableBodyCell>
        </TableBodyRow>
  
        {#if openRow === i}
          <TableBodyRow on:dblclick={() => openModal(item)}>
            <td colspan="4" class="p-0">
              <div class="px-2 py-3" transition:slide={{ duration: 300, axis: 'y' }}>
                <ImagePlaceholder />
              </div>
            </td>
          </TableBodyRow>
        {/if}
      {/each}
    </TableBody>
  </Table>
  
  <!-- Modal hanya muncul jika doubleClickModal aktif -->
  {#if doubleClickModal}
    <Modal title={details ? details.name : ''} bind:open={doubleClickModal} autoclose outsideclose>
      {#if details}
        <ImagePlaceholder />
      {/if}
    </Modal>
  {/if}
  