<template>
	<div>
		<v-app>
			<div class="d-flex">
			<v-navigation-drawer
				color="muted"
				permanent>
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
			<v-col class="mx-auto">
					<nuxt-child 
						:id_perusahaan="id_perusahaan"/>
				</v-col>
			</div>
		</v-app>
		
	</div>
</template>
<script>
export default {
	async asyncData({ params }){
		return {
			id_perusahaan: params.id
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
			{ title: 'Cetak', icon: 'mdi-printer', to:"/cetak" },
        ],
        right: null,
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
