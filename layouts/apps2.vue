<template>
	<v-app>
		<v-navigation-drawer
			v-model="drawer"
			:mini-variant="miniVariant"
			:clipped="clipped"
			permanent
			expand-on-hover
			app>

			<v-list>
				<v-list-item class="px-2">
					<v-list-item-avatar>
						<v-img :src="user.picture"></v-img>
					</v-list-item-avatar>
				</v-list-item>

				<v-list-item link>
					<v-list-item-content>
					<v-list-item-title class="title">
						Si Bungkil
					</v-list-item-title>
					<v-list-item-subtitle>{{ user.name }}</v-list-item-subtitle>
					</v-list-item-content>
				</v-list-item>
			</v-list>

			<v-divider></v-divider>

			<v-list>
				<v-list-item
					color="primary"
					to="/apps/beranda">
					<v-list-item-action>
						<v-icon>mdi-apps</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="'Beranda'" />
					</v-list-item-content>
				</v-list-item>
				<v-list-item
					v-for="(item, i) in apps[tipe]"
					:key="i"
					:to="item.link"
					color="primary">
					<v-list-item-action>
						<v-icon>{{ item.ikon }}</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="item.nama" />
					</v-list-item-content>
				</v-list-item>
				<v-list-item
					color="primary"
					to="/">
					<v-list-item-action>
						<v-icon>mdi-logout</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="'Keluar'" />
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>

		<v-main>
			<v-container>
				<nuxt-child :apps="apps[tipe]"/>
			</v-container>
		</v-main>

		<v-navigation-drawer
		v-model="rightDrawer"
		:right="right"
		temporary
		fixed
		>
		<v-list>
			<v-list-item @click.native="right = !right">
			<v-list-item-action>
				<v-icon light>
				mdi-repeat
				</v-icon>
			</v-list-item-action>
			<v-list-item-title>Switch drawer (click me)</v-list-item-title>
			</v-list-item>
		</v-list>
		</v-navigation-drawer>
		<v-footer
		:absolute="!fixed"
		app
		>
		<span>&copy; {{ new Date().getFullYear() }} Si Bungkil</span>
		</v-footer>
	</v-app>
</template>

<script>
export default {
	data () {
		let user = this.$auth.user
		let tipe = this.$auth.$storage.getUniversal("loginType")
		if(!user){
			this.$router.push(`/`) 
		}
		return {
			user,
			tipe,
			clipped: false,
			drawer: false,
			fixed: false,
			apps:{
				admin: [
					{
						"ikon": "mdi-domain",
						"nama":"Perusahaan",
						"deskripsi":"Sistem Pengelolaan informasi perusahaan",
						"link":"/apps/perusahaan"
					},
					{
						"ikon": "mdi-bullhorn",
						"nama":"Pengumuman",
						"deskripsi":"Pengumuman untuk semua perusahaan",
						"link":"/apps/pengumuman"
					},
					{
						"ikon": "mdi-cash-multiple",
						"nama":"Keuangan",
						"deskripsi":"Sistem Pengelolaan Data Keuangan Terpadu",
						"link":"/apps/keuangan"
					},
					{
						"ikon": "mdi-account-tie",
						"nama":"Kepegawaian",
						"deskripsi":"Sistem Pengelolaan Data Kepegawaian Terpadu",
						"link":"/apps/kepegawaian"
					},
					{
						"ikon": "mdi-calendar-clock",
						"nama":"Kehadiran",
						"deskripsi":"Sistem Pengelolaan Data Kehadiran Terpadu",
						"link":"/apps/kehadiran"
					},
					{
						"ikon": "mdi-book-open-variant",
						"nama":"LMS",
						"deskripsi":"Learning Mangement System untuk pegawai baru",
						"link":"/apps/lms"
					},
				],
				perusahaan: [
					{ nama: 'Pengumuman', ikon: 'mdi-bullhorn', link:"/apps/pengumuman" },
					{ nama: 'Data Perusahaan', ikon: 'mdi-view-dashboard', link:"/apps/perusahaan/1/perusahaan" },
					{ nama: 'Legalitas', ikon: 'mdi-file', link:"/apps/perusahaan/1/legalitas" },
					{ nama: 'Lahan Pembibitan', ikon: 'mdi-map-marker-multiple', link:"/apps/perusahaan/1/pembibitan" },
					{ nama: 'Penyelesaian HAT', ikon: 'mdi-map-check-outline', link:"/apps/perusahaan/1/penyelesaianhat" },
					{ nama: 'Pembukaan Lahan', ikon: 'mdi-map-check', link:"/apps/perusahaan/1/pembukaan" },
					{ nama: 'Penanaman Lahan', ikon: 'mdi-map-clock', link:"/apps/perusahaan/1/penanaman" },
					{ nama: 'Tenaga Kerja', ikon: 'mdi-account-hard-hat', link:"/apps/perusahaan/1/tenagakerja" },
					{ nama: 'Pembangunan Pabrik', ikon: 'mdi-hammer-wrench', link:"/apps/perusahaan/1/pembangunanpabrik" },
					{ nama: 'Kendali Kebakaran', ikon: 'mdi-fire', link:"/apps/perusahaan/1/kendalikebakaran" },
					{ nama: 'Kendali OPT', ikon: 'mdi-tower-fire', link:"/apps/perusahaan/1/kendaliopt" },
					{ nama: 'Sarana Produksi', ikon: 'mdi-warehouse', link:"/apps/perusahaan/1/saranaproduksi" },
					{ nama: 'Alat Berat', ikon: 'mdi-excavator', link:"/apps/perusahaan/1/alatberat" },
					{ nama: 'Prasarana Sosial', ikon: 'mdi-charity', link:"/apps/perusahaan/1/prasaranasosial" },
					{ nama: 'Produksi', ikon: 'mdi-hammer', link:"/apps/perusahaan/1/produksi" },
					{ nama: 'Pemasaran', ikon: 'mdi-shopping', link:"/apps/perusahaan/1/pemasaran" },
					{ nama: 'Kerjasama Kemitraan', ikon: 'mdi-handshake', link:"/apps/perusahaan/1/kerjasamamitra" },
					{ nama: 'Kemitraan Lainnya', ikon: 'mdi-handshake-outline', link:"/apps/perusahaan/1/kemitraanlainnya" },
					{ nama: 'CSR', ikon: 'mdi-gift', link:"/apps/perusahaan/1/csr" },
					{ nama: 'Permasalahan', ikon: 'mdi-folder-alert', link:"/apps/perusahaan/1/permasalahan" },
					{ nama: 'Galeri', ikon: 'mdi-image-multiple', link:"/apps/perusahaan/1/galeri" },
					{ nama: 'Cetak', ikon: 'mdi-printer', link:"/apps/perusahaan/1/cetak" },
				],
			},
			miniVariant: false,
			right: true,
			rightDrawer: false,
			title: 'Si Bungkil'
		}
	},
	methods:{
		getApps: function (){
			return this.apps[this.tipe]
		}
	}
}
</script>
<style>
.border--primary{
	border: 1px solid #FF6D00!important
}
</style>