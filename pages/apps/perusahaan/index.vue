<template>
	<div>
		<Head 
			title="Perusahaan" 
			subtitle="Modul Perusahaan untuk kelola data perusahaan"
			color="text--black">
			<v-btn v-on:click="dialogForm=true" small class="d-xs-none">
                <v-icon left>mdi-plus-circle</v-icon>
                Tambah
            </v-btn>
		</Head>
		<GMap
			style="margin-left: -32px; margin-right: -32px;"
			ref="gMap"
			language="id"
			:cluster="{options: {styles: clusterStyle}}"
			:center="{lat: -0.897788, lng: 117.5383008}"
			:options="{fullscreenControl: true}"
			:zoom="5.27"
			>
				<GMapMarker
					v-for="(location, index) in data.filter((item)=>item.lokasi_kebun_lat!='' || item.lokasi_kebun_lat!=null)"
					:key="index"
					:position="{lat: location.lokasi_kebun_lat, lng: location.lokasi_kebun_lng}"
					@click="currentLocation = location">
						<GMapInfoWindow :options="{maxWidth: 200}">
						<code>
							{{ location.nama }}
						</code>
						</GMapInfoWindow>
				</GMapMarker>
				<GMapCircle :options="circleOptions"/>
			</GMap>
		<v-row justify="center" class="mt-2">
			<CardStats 
				sm="12" 
				md="3"
				title="Total Perusahaan" 
				:value="dataDasbor.total_perusahaan"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Luas Lokasi"
				:value="dataDasbor.luas_lokasi||0"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total Luas PPUB"
				:value="dataDasbor.luas_ppub||0"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total. IPL" 
				:value="dataDasbor.luas_ipl||0"/>
		</v-row>
		<v-data-table
			dense
			:headers="headers"
			:items="data"
			item-key="name"
			class="elevation-1 mt-6"
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
			<template v-slot:[`item.dibuat`]="{item}">
				{{$moment(item.dibuat).format('DD MMM, HH:mm:ss')}}
			</template>
			<template v-slot:[`item.diubah`]="{item}">
				{{item.diubah!=null ? $moment(item.diubah).format('DD MMM, HH:mm:ss'): '-'}}
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<!-- <v-btn small icon to="/apps/perusahaan/data/tambah/cetak">
					<v-icon small>
						mdi-printer
					</v-icon>
				</v-btn> -->
				<v-btn 
					small 
					icon 
					:to="`/apps/perusahaan/${item.id}`">
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
				<v-card-title class="headline">Apakah anda yakin ingin menghapus data perusahaan ini ?</v-card-title>
				<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn 
					text 
					color="blue darken-1" 
					v-on:click="dialogDelete=false">Batal</v-btn>
				<v-btn 
					text 
					color="blue darken-1" 
					v-on:click="handleHapus">OK</v-btn>
				<v-spacer></v-spacer>
				</v-card-actions>
			</v-card>
		</v-dialog>
		<v-dialog
			v-model="dialogForm"
			persistent
			max-width="600px">
			<v-card>
				<v-card-title>
					<span class="text-h5">Tambah Perusahaan</span>
				</v-card-title>
				<v-card-text>
					<v-container>
						<v-text-field
							v-model="formData.nama"
							label="Nama Perusahaan*"
							required
							hint="Contoh: PT. ABC 123"/>
					
						<v-text-field
							v-model="formData.email_pengelola"
							label="Email Pengelola*"
							hint="Contoh: email@gmail.com"
							required/>
					</v-container>
				<small>*indicates required field</small>
				</v-card-text>
				<v-card-actions>
					<v-spacer></v-spacer>
					<v-btn
						color="blue darken-1"
						text
						v-on:click="dialogForm = false">
						Batal
					</v-btn>
					<v-btn
						color="blue darken-1"
						text
						v-on:click="handleTambahPerusahaan"
						:disabled="formData.nama==='' || formData.email_pengelola===''">
						Simpan
					</v-btn>
				</v-card-actions>
			</v-card>
		</v-dialog>
		<v-dialog
			v-model="isFetching"
			hide-overlay
			persistent
			width="300">
			<v-card
				color="primary"
				dark>
				<v-card-text>
				Memproses
				<v-progress-linear
					indeterminate
					color="white"
					class="mb-0"
				></v-progress-linear>
				</v-card-text>
			</v-card>
		</v-dialog>
		<v-dialog
            v-if="alert.show"
			v-model="alert.show"            
			width="300">
			<v-alert
                v-model="alert.show"
                border="top"
                color="green accent-4"
                dark
                dismissible
                type="success"
                >
                {{ alert.message }}
            </v-alert>
		</v-dialog>
	</div>
</template>
<script>
export default {
	mounted: function(){
		this.handleUpdateDataDasbor()
		this.handleUpdateData()
	},
	data: ()=>({
		currentLocation: {},
		circleOptions: {
		
		},
		locations: [
			{
				lat: 44.933076,
				lng: 15.629058
			},
			{
				lat: 45.815,
				lng: "15.9819"
			},
			{
				lat: "45.12",
				lng: "16.21"
			}
		],
		mapStyle: [],
		clusterStyle: [
			{
				url: "https://developers.google.com/maps/documentation/javascript/examples/markerclusterer/m1.png",
				width: 56,
				height: 56,
				textColor: "#fff"
			}
		],


		dataDasbor: {},
		isFetching:false,
		dialogForm:false,
		formData:{
			nama: '',
			email_pengelola:'',
		},
		alert: {
			show:false,
			message: ''
		},
		dialogDelete: false,
		data: [],
		perusahaan: {},
		headers: [
			{ text: 'Nama Perusahaan', value: 'nama' },
			{ text: 'Kantor Pusat', value: 'alamat_kantor_pusat' },
			{ text: 'Dibuat', value: 'dibuat' },
			{ text: 'Diubah', value: 'diubah' },			
			{ text: 'Aksi', value: 'aksi' },
		],
		opsiPencarian: ['Nama Perusahaan', 'NPWP', 'Nama Kebun'],
	}),
	methods:{
		handleKonfirmasiHapus(item){
			// console.log(this)
			this.perusahaan		= item
			this.dialogDelete	= true
		},
		handleHapus(){
			this.isFetching		= true
			this.$api.$get(`/v1/api/hapus/perusahaan/${this.perusahaan.id}`).then((resp)=>{
				this.isFetching	= false
				this.alert		= {
					show:true,
					message:"Data perusahaan berhasil ditambahkan"
				}
				if(resp.status){
					this.handleUpdateData()
					this.dialogForm	= false
				}
			})
			this.dialogDelete	= false
		},
		async handleUpdateData(){
			const data 	= (await this.$api.$get('/v1/api/data/perusahaan'))
			this.data	= data.data
		},
		handleTambahPerusahaan(){
			this.isFetching		= true
			this.$api.$post('/v1/api/tambah/perusahaan', this.formData).then((resp)=>{
				this.isFetching	= false
				this.alert		= {
					show:true,
					message:"Data perusahaan berhasil ditambahkan"
				}
				if(resp.status){
					this.handleUpdateData()
					this.dialogForm	= false
					this.formData	= {
							nama: '',
							email_pengelola:'',
						}
				}
			})
		},
		async handleUpdateDataDasbor(){
			const data 		= (await this.$api.$get('/v1/api/dasborPerusahaan'))
			this.dataDasbor	= data.data
		},
	}
	
}
</script>