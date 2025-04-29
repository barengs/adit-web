<script>
 
  import { Table, TableBody, TableBodyCell, TableBodyRow, TableHead, TableHeadCell } from 'flowbite-svelte';
  let items = [
    { id: 1, nama: 'yota', prodi:'TI', status: 'LULUS' },
    { id: 2, nama: 'riza', prodi:'SI', status: 'TIDAK LULUS' },
    { id: 3, nama: 'akbar', prodi:'SI', status: 'LULUS' },
    { id: 4, nama: 'rindi', prodi:'TI', status: 'TIDAK LULUS' }
    
  ];
</script>







<Table {items} placeholder="cari nama" hoverable={true} filter={(item, searchTerm) => item.nama.toLowerCase().includes(searchTerm.toLowerCase())}>
  <TableHead>
    <TableHeadCell>ID</TableHeadCell>
    <TableHeadCell>NAMA</TableHeadCell>
    <TableHeadCell>PRODI</TableHeadCell>
    <TableHeadCell>STATUS</TableHeadCell>
  </TableHead>
  <TableBody tableBodyClass="divide-y">
    <TableBodyRow slot="row" let:item>
      <TableBodyCell>{item.id}</TableBodyCell>
      <TableBodyCell>{item.nama}</TableBodyCell>
      <TableBodyCell>{item.prodi}</TableBodyCell>
      <TableBodyCell>{item.status}</TableBodyCell>
    </TableBodyRow>
  </TableBody>
</Table>