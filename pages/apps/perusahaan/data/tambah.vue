<template>
	<div>
		<Head 
			title="Tambah" 
			subtitle="Tambah Data Perusahaan"
			back/>
		<v-app>
			<div class="d-flex">
			<v-navigation-drawer>
				
				<v-list
					dense
					nav
				>
					<v-list-item
						v-for="item in items"
						:key="item.title"
						:to="`/apps/perusahaan/data/tambah${item.to}`"
						link
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
			<v-main style="min-height:100vh">
				<v-container>
				<v-col class="mx-auto">
					<nuxt/>
				</v-col>
				</v-container>
			</v-main>
			</div>
		</v-app>
		
	</div>
</template>
<script>
export default {
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
			{ title: 'Data Perusahaan', icon: 'mdi-view-dashboard', to:"" },
			{ title: 'Legalitas', icon: 'mdi-file', to:"/legalitas" },
			{ title: 'Lahan Pembibitan', icon: 'mdi-map-marker-multiple', to:"/pembibitan" },
			{ title: 'Penyelesaian HAT', icon: 'mdi-map-check-outline', to:"/penyelesaianhat" },
			{ title: 'Pembukaan Lahan', icon: 'mdi-map-check' },
			{ title: 'Penanaman', icon: 'mdi-map-clock' },
			{ title: 'Tenaga Kerja', icon: 'mdi-account-hard-hat' },
			{ title: 'Pembangunan Pabrik', icon: 'mdi-hammer-wrench' },
			{ title: 'Kendali Kebakaran', icon: 'mdi-fire' },
			{ title: 'Kendali OPT', icon: 'mdi-tower-fire' },
			{ title: 'Sarana Produksi', icon: 'mdi-warehouse' },
			{ title: 'Alat Berat', icon: 'mdi-excavator' },
			{ title: 'Produksi', icon: 'mdi-hammer' },
			{ title: 'Pemasaran', icon: 'mdi-shopping' },
			{ title: 'Kerjasama Kemitra', icon: 'mdi-handshake' },
			{ title: 'Kemitraan Lainnya', icon: 'mdi-handshake-outline' },
        ],
        right: null,
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
