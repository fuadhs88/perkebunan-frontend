<template>
	<div>
		<Crud
			:crud="crud"/>
	</div>
</template>
<script>
export default {
	data: () => ({
		crud:{
			title: "Kelompok",
			subtitle: "Kelola Kelompok Penerimaan Peserta Didik Baru",
			headers: [
				{
					text: 'Kelompok',
					value: 'kelompok',
					info: ['Kelompok penerimaan, contoh: Jalur Prestasi, Jalur Zonasi']
				}, 
				{
					text: 'Kapasitas',
					value: 'kapasitas',
					type: 'number',
					info: ['Jumlah siswa yang akan diterima, contoh: 100']
				}, 
				{
					text: 'Terisi',
					value: 'terisi',
					type: 'number',
					info: ['Jumlah siswa yang sudah diterima sementara, Contoh: 10']
				}, 
				{
					text: 'Keterangan',
					value: 'keterangan',
					info: ['Keterangan tambahan pada kelompok ini'],
				},
				{
					text: 'Aksi',
					value: 'aksi',
					form: false
				}
			],
			data:[
				{
					kelompok: "Jalur Prestasi",
					kapasitas: 40,
					terisi: 0,
					keterangan: "-",
				},
				{
					kelompok: "Jalur Zonasi",
					kapasitas: 40,
					terisi: 0,
					keterangan: "-",
				},
			]
		}
    }),
	methods:{
		
	}
}
</script>
