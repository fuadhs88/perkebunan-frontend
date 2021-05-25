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
			title: "Akun",
			subtitle: "Kelola Akun Login Perusahaan",
			headers: [
				{
					text: 'Nama Perusahaan',
					value: 'perusahaan',
					info: ['Nama proses PPDB, Contoh : Samsung LTD']
				}, 
				{
					text: 'Username',
					value: 'username',
					info: ['Username akun perusahaan, contoh samsung56'],
				}, 
				{
					text: 'Password',
					value: 'password',
					info: ['Password akun perusahaan, gunakan kombinasi angka dan huruf: 54abc']
				}, 
				{
					text: 'Aktif ?',
					value: 'status',
					type: 'switch'
				}, 
				{
					text: 'Aksi',
					value: 'aksi',
					form: false
				}
			],
			data: [
				{
					id:"1",
					perusahaan: "Perusahaan ABC",
					username: "samsung1256",
					password: "qrgjs79",
					status: 1,
				},
				{
					id:"2",
					perusahaan: "Perusahaan EFG",
					username: "sony1256",
					password: "qrgjs79",
					status: 1,
				},
			]
		}
    }),
	methods:{
		
	}
}
</script>
