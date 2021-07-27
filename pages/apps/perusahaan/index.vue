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
			v-if="data.length>0"
			style="margin-left: -32px; margin-right: -32px;"
			ref="gMap"
			language="id"
			:center="{lat: -0.897788, lng: 117.5383008}"
			:options="{fullscreenControl: true}"
			:zoom="5.27">
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
		<v-card class="mt-2">
			<v-simple-table dense class="mt-2">
			<template v-slot:default>
			<thead>
				<tr>
					<th>Total Perusahaan: <b>{{ dataDasbor.total_perusahaan }}</b></th>
					<th width="100px">TR 1</th>
					<th width="100px">TR 2</th>
					<th width="100px">TR 3</th>
					<th width="100px">TR 4</th>
				</tr>
			</thead>
			<tbody>
				<tr>
					<td>Luas Lokasi</td>
					<td>{{ dataDasbor.lokasi.triwulan1 }}</td>
					<td>{{ dataDasbor.lokasi.triwulan2 }}</td>
					<td>{{ dataDasbor.lokasi.triwulan3 }}</td>
					<td>{{ dataDasbor.lokasi.triwulan4 }}</td>
				</tr>
				<tr>
					<td>Luas IUP/PPUB</td>
					<td>{{ dataDasbor.ppub.triwulan1 }}</td>
					<td>{{ dataDasbor.ppub.triwulan2 }}</td>
					<td>{{ dataDasbor.ppub.triwulan3 }}</td>
					<td>{{ dataDasbor.ppub.triwulan4 }}</td>
				</tr>
				<tr>
					<td>Luas IPL</td>
					<td>{{ dataDasbor.ipl.triwulan1 }}</td>
					<td>{{ dataDasbor.ipl.triwulan2 }}</td>
					<td>{{ dataDasbor.ipl.triwulan3 }}</td>
					<td>{{ dataDasbor.ipl.triwulan4 }}</td>
				</tr>
				<tr>
					<td>Jumlah Koperasi</td>
					<td>{{ dataDasbor.koperasi.triwulan1 }}</td>
					<td>{{ dataDasbor.koperasi.triwulan2 }}</td>
					<td>{{ dataDasbor.koperasi.triwulan3 }}</td>
					<td>{{ dataDasbor.koperasi.triwulan4 }}</td>
				</tr>
				<tr>
					<td>TM Kemitraan</td>
					<td>{{ dataDasbor.koperasi_tm.triwulan1 }}</td>
					<td>{{ dataDasbor.koperasi_tm.triwulan2 }}</td>
					<td>{{ dataDasbor.koperasi_tm.triwulan3 }}</td>
					<td>{{ dataDasbor.koperasi_tm.triwulan4 }}</td>
				</tr>
				<tr>
					<td>TBM Kemitraan</td>
					<td>{{ dataDasbor.koperasi_tbm.triwulan1 }}</td>
					<td>{{ dataDasbor.koperasi_tbm.triwulan2 }}</td>
					<td>{{ dataDasbor.koperasi_tbm.triwulan3 }}</td>
					<td>{{ dataDasbor.koperasi_tbm.triwulan4 }}</td>
				</tr>
				<tr>
					<td>TBS INTI / ton</td>
					<td>{{ dataDasbor.inti_tbs.triwulan1 }}</td>
					<td>{{ dataDasbor.inti_tbs.triwulan2 }}</td>
					<td>{{ dataDasbor.inti_tbs.triwulan3 }}</td>
					<td>{{ dataDasbor.inti_tbs.triwulan4 }}</td>
				</tr>
				<tr>
					<td>TBS PLASMA / ton</td>
					<td>{{ dataDasbor.plasma_tbs.triwulan1 }}</td>
					<td>{{ dataDasbor.plasma_tbs.triwulan2 }}</td>
					<td>{{ dataDasbor.plasma_tbs.triwulan3 }}</td>
					<td>{{ dataDasbor.plasma_tbs.triwulan4 }}</td>
				</tr>
			</tbody>
			</template>
		</v-simple-table>
		</v-card>
		
		<!-- <v-row justify="center" class="mt-2">
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
				title="Total Luas IUP/PPUB"
				:value="dataDasbor.luas_ppub||0"/>
			<CardStats 
				sm="12" 
				md="3"
				title="Total. IPL" 
				:value="dataDasbor.luas_ipl||0"/>
		</v-row> -->
		<v-data-table
			dense
			:headers="headers"
			:items="data"
			item-key="name"
			class="elevation-1 mt-6"
			height="65vh"
			:search="keyword">
			<template v-slot:top>
				<v-container>
				<v-row dense>
					<v-col cols="12" md="3">
						<v-select
							dense
							v-model="tahunDipilih"
							item-text="label"
							item-value="value"
							:items="[2021]"
							label="Tahun Laporan"/>
					</v-col>
					<v-col cols="12" md="6">
						<v-text-field
							dense
							v-model="keyword"
							label="Keyword"/>
					</v-col>
					<v-col cols="12" md="3">
						<v-btn small block>
							Cari
							<v-icon small right>
								mdi-account-search-outline
							</v-icon>
						</v-btn>
					</v-col>
				</v-row>
				</v-container>
			</template>
			<template v-slot:[`item.triwulan1`]="{item}">
				<v-icon small v-if="item.triwulan1===null || item.triwulan1==='belum'" color="error">
					mdi-radiobox-blank
				</v-icon>
				<v-icon small v-else color="success">
					mdi-check-all
				</v-icon>
			</template>
			<template v-slot:[`item.triwulan2`]="{item}">
				<v-icon small v-if="item.triwulan2===null || item.triwulan2==='belum'" color="error">
					mdi-radiobox-blank
				</v-icon>
				<v-icon small v-else color="success">
					mdi-check-all
				</v-icon>
			</template>
			<template v-slot:[`item.triwulan3`]="{item}">
				<v-icon small v-if="item.triwulan3===null || item.triwulan3==='belum'" color="error">
					mdi-radiobox-blank
				</v-icon>
				<v-icon small v-else color="success">
					mdi-check-all
				</v-icon>
			</template>
			<template v-slot:[`item.triwulan4`]="{item}">
				<v-icon small v-if="item.triwulan4===null || item.triwulan4==='belum'" color="error">
					mdi-radiobox-blank
				</v-icon>
				<v-icon small v-else color="success">
					mdi-check-all
				</v-icon>
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
	watch: {
		tahunDipilih: function(){
			this.handleUpdateDataDasbor()
		}
	},
	mounted: function(){
		this.handleUpdateDataDasbor()
		this.handleUpdateData()
	},
	data: ()=>({
		tahunDipilih: 2021,
		keyword:'',
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


		dataDasbor: {
			lokasi: {},
			ppub: {},
			ipl: {},
			koperasi: {},
			koperasi_tm: {},
			koperasi_tbm: {},
			pabrik: {},
			inti_tbs: {},
			plasma_tbs: {},
		},
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
			{ text: 'Tr 1', value: 'triwulan1' },			
			{ text: 'Tr 2', value: 'triwulan2' },			
			{ text: 'Tr 3', value: 'triwulan3' },			
			{ text: 'Tr 4', value: 'triwulan4' },			
			{ text: 'Aksi', value: 'aksi' },
		],
		opsiPencarian: ['Nama Perusahaan', 'NPWP', 'Nama Kebun', 'Status Pengisian'],
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
					message:"Data perusahaan berhasil dihapus"
				}
				if(resp.status){
					this.handleUpdateData()
					this.dialogForm	= false
				}
			})
			this.dialogDelete	= false
		},
		async handleUpdateData(){
			const data 			= (await this.$api.$get(`/v1/api/perusahaanTriwulan/${this.tahunDipilih}`))
			this.data			= data.data

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
					console.log(this.$router)
					this.$router.app.refresh()
				}
			})
		},
		async handleUpdateDataDasbor(){
			const data 		= (await this.$api.$get(`/v1/api/dasborPerusahaan/${this.tahunDipilih}`))
			this.dataDasbor	= data.data
		},
	}
	
}
</script>