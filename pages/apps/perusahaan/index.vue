<template>
	<div>
		<Head 
			title="Dashboard" 
			subtitle="Statistik Data Perusahaan"/>
		
		<v-row justify="center">
			<CardStats 
				sm="12" 
				md="3"
				title="Total Perusahaan" 
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Luas Lokasi"
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Luas Lokasi"
				value="200"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total. IPL" 
				value="200"/>
		</v-row>

		<Head 
			title="Memulai" 
			subtitle="Berikut langkah-langkah untuk mengelola data perusahaan"/>
			
		<CardStep
			:instruksi="instruksi"
			:instruksiAktif="instruksiAktif"/>
		
	</div>
</template>
<script>
export default {
	data: ()=>({
		instruksiAktif:1,
		instruksi:[
			{
				judul: "Setup data akun perusahaan",
				instruksi: "Membuat akun perusahaan, agar perusahaan dapat update data. Contoh : Perusahaan PT ABC,",
			},
			{
				judul: "Kelola data perusahaan",
				instruksi: "Melihat laporan data perusahaan",
			},
			{
				judul: "Pelaporan",
				instruksi: "Cetak laporan data perusahaan",
			},
		]
	})
}
</script>