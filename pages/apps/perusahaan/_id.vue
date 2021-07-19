<template>
	<div>
		<v-app>
			<div class="d-flex">
			<v-navigation-drawer
				class="d-none d-lg-flex"
				color="muted"
				permanent
				>
				<v-list
					dense
					nav>
					<v-list-item
						v-for="item in items"
						:key="item.title"
						:to="`/apps/perusahaan/${id_perusahaan}${item.to}`"
						link
						color="primary"
						>
					<v-list-item-icon>
						<v-icon>{{ item.icon }}</v-icon>
					</v-list-item-icon>

					<v-list-item-content>
						<v-list-item-title>{{ item.title }}</v-list-item-title>
					</v-list-item-content>
					</v-list-item>
				</v-list>
			</v-navigation-drawer>				
				<v-col>
					<v-row>
					<v-col cols="12" md="4">
						<v-select
							v-model="tahunDipilih"
							label="Tahun Dipilih"
							:items="[2021]"/>
					</v-col>
					<v-col cols="12" md="8">
						<v-chip-group
							active-class="primary--text"
							column
							v-model="triwulanDipilih">
							<v-chip
							v-for="(item, key) in ['Triwulan 1', 'Triwulan 2',  'Triwulan 3', 'Triwulan 4']"
							:key="key"
							>
							{{ item }}
							</v-chip>
						</v-chip-group>
					</v-col>
					</v-row>
					<nuxt-child 
						:id_perusahaan="id_perusahaan"
						:triwulan="getTriwulan()"/>
				</v-col>
			</div>
		</v-app>
		
	</div>
</template>
<script>
export default {
	async asyncData({ params }){
		return {
			tahunDipilih: 2021,
			id_perusahaan: params.id,
			triwulanDipilih: 0,
		}
	},
	data: () => ({
		valid: false,
		rule:{
			name:[
				v => !!v || 'Username harus diisi',
			],
			password:[
				v => !!v || 'Password harus diisi',
			]
		},
		items: [
			{ title: 'Data Perusahaan', icon: 'mdi-view-dashboard', to:"/perusahaan" },
			{ title: 'Legalitas', icon: 'mdi-file', to:"/legalitas" },
			{ title: 'Lahan Pembibitan', icon: 'mdi-map-marker-multiple', to:"/pembibitan" },
			{ title: 'Penyelesaian HAT', icon: 'mdi-map-check-outline', to:"/penyelesaianhat" },
			{ title: 'Pembukaan Lahan', icon: 'mdi-map-check', to:"/pembukaan" },
			{ title: 'Penanaman Lahan', icon: 'mdi-map-clock', to:"/penanaman" },
			{ title: 'ANKT', icon: 'mdi-format-list-checkbox', to:"/ankt" },
			{ title: 'Lahan Gambut', icon: 'mdi-format-list-numbered', to:"/lahangambut" },
			{ title: 'Embung', icon: 'mdi-format-list-bulleted', to:"/embung" },
			{ title: 'Tenaga Kerja', icon: 'mdi-account-hard-hat', to:"/tenagakerja" },
			{ title: 'Pembangunan Pabrik', icon: 'mdi-hammer-wrench', to:"/pembangunanpabrik" },
			{ title: 'Kendali Kebakaran', icon: 'mdi-fire', to:"/kendalikebakaran" },
			{ title: 'Kendali OPT', icon: 'mdi-tower-fire', to:"/kendaliopt" },
			{ title: 'Sarana Produksi', icon: 'mdi-warehouse', to:"/saranaproduksi" },
			{ title: 'Alat Berat', icon: 'mdi-excavator', to:"/alatberat" },
			{ title: 'Prasarana Sosial', icon: 'mdi-charity', to:"/prasaranasosial" },
			{ title: 'Produksi', icon: 'mdi-hammer', to:"/produksi" },
			{ title: 'Pemasaran', icon: 'mdi-shopping', to:"/pemasaran" },
			{ title: 'Kerjasama Kemitraan', icon: 'mdi-handshake', to:"/kerjasamamitra" },
			{ title: 'Kemitraan Lainnya', icon: 'mdi-handshake-outline', to:"/kemitraanlainnya" },
			{ title: 'CSR', icon: 'mdi-gift', to:"/csr" },
			{ title: 'Permasalahan', icon: 'mdi-folder-alert', to:"/permasalahan" },
			{ title: 'Galeri', icon: 'mdi-image-multiple', to:"/galeri" },
			{ title: 'Konfirmasi Selesai', icon: 'mdi-check-all', to:"/konfirmasi" },
			{ title: 'Cetak Laporan', icon: 'mdi-printer', to:"/cetak" },
			{ title: 'Cetak Serah Terima', icon: 'mdi-printer-check', to:"/serahterima" },
        ],
        right: null,
    }),
	methods:{
		getTriwulan: function(){
			return `${this.tahunDipilih}${this.triwulanDipilih+1}`
		}
	}
}
</script>
