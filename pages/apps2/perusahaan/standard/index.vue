<template>
	<div>
		<Head 
			title="Proses" 
			subtitle="Kelola Proses Penerimaan Peserta Didik Baru"
			add="/apps/ppdb/proses/tambah"
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
			<template v-slot:[`item.status`]="{item}">
				<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon to="/apps/ppdb/proses/edit">
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
				proses: "Penerimaan Siswa Baru 2020",
				kode: "2020",
				jumlah_penerimaan: 300,
				keterangan: "-",
				status: 1,
			},
			{
				id:"2",
				proses: "Penerimaan Siswa Baru 2021",
				kode: "2021",
				jumlah_penerimaan: 320,
				keterangan: "-",
				status: 1,
			},
		],
		headers: [
			{ text: 'Proses', value: 'proses' },
			{ text: 'Kode Awalan', value: 'kode' },
			{ text: 'Jumlah Penerimaan', value: 'jumlah_penerimaan' },
			{ text: 'Keterangan', value: 'keterangan' },
			{ text: 'Status', value: 'status' },
			{ text: 'Aksi', value: 'aksi' },
		],
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
