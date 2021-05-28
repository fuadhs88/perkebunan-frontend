<template>
	<div>
		<Head 
			title="Perusahaan" 
			subtitle="Kelola data perusahaan"
			add="/apps/perusahaan/data/tambah"
			:handleDelete="dipilih.length>0 && handleKonfirmasiHapus"/>
		<v-data-table
			dense
			v-model="dipilih"
			:headers="headers"
			:items="data"
			item-key="name"
			show-select
			class="elevation-1"
			height="65vh">
			<template v-slot:top>
				<div class="d-flex px-4 pt-4 align-center">
					<v-select
					:items="opsiPencarian"
					label="Pilih Opsi Pencarian"/>
					<v-text-field
						label="Keyword"/>
					<v-btn class="ml-4">
						<div class="px-12">
							Cari
							<v-icon small right>
								mdi-account-search-outline
							</v-icon>
						</div>
					</v-btn>
				</div>
				
			</template>
			<template v-slot:[`item.status`]="{item}">
				<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon to="/apps/perusahaan/data/tambah/cetak">
					<v-icon small>
						mdi-printer
					</v-icon>
				</v-btn>
				<v-btn small icon to="/apps/perusahaan/data/tambah">
					<v-icon small>
						mdi-pencil
					</v-icon>
				</v-btn>
				<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
					<v-icon small>
						mdi-delete
					</v-icon>
				</v-btn>
			</template>
		</v-data-table>
		<v-dialog v-model="dialogDelete" max-width="500px">
			<v-card>
				<v-card-title class="headline">Apakah anda yakin ingin menghapus data ini ?</v-card-title>
				<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue darken-1" text @click="dialogDelete=false">Batal</v-btn>
				
				<v-btn color="blue darken-1" text @click="handleHapus">OK</v-btn>
				<v-spacer></v-spacer>
				</v-card-actions>
			</v-card>
		</v-dialog>
		
	</div>
</template>
<script>
export default {
	data: () => ({
		dipilih: [],
		dialogDelete: false,
		data: [
			{
				id:"1",
				nama: "PT Sawit Medan",
				npwp: "1202144193",
				nama_kebun: "Perkebunan Sawit Medan",
				desa: "Desa A",
				kecamatan: "Kecamatan A",
				kabupaten: "Kabupaten A",
				provinsi: "Jawa Barat",
				status: 1,
			},
			{
				id:"1",
				nama: "PT Duren Medan",
				npwp: "1202144193",
				nama_kebun: "Perkebunan Duren ABC",
				desa: "Desa A",
				kecamatan: "Kecamatan A",
				kabupaten: "Kabupaten A",
				provinsi: "Jawa Barat",
				status: 1,
			},
		],
		headers: [
			{ text: 'Nama Perusahaan', value: 'nama' },
			{ text: 'NPWP', value: 'npwp' },
			{ text: 'Nama Kebun', value: 'nama_kebun' },
			{ text: 'Desa', value: 'desa' },
			{ text: 'Kecamatan', value: 'kecamatan' },
			{ text: 'Kabupaten', value: 'kabupaten' },
			{ text: 'Provinsi', value: 'provinsi' },
			{ text: 'Status', value: 'status' },
			{ text: 'Aksi', value: 'aksi' },
		],
		opsiPencarian: ['Nama Perusahaan', 'NPWP', 'Nama Kebun'],
    }),
	methods:{
		handleKonfirmasiHapus(){
			// console.log(this)
			this.dialogDelete	= true
		},
		handleHapus(){
			this.dialogDelete	= false
		}
	}
}
</script>
