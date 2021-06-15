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
					v-for="(item, i) in apps"
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
				<nuxt/>
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
			apps:[
				{
					"ikon": "mdi-domain",
					"nama":"Perusahaan",
					"deskripsi":"Sistem Pengelolaan informasi perusahaan",
					"link":"/apps/perusahaan"
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
					"link":"ppdb",
					"link":"/apps/kehadiran"
				},
				{
					"ikon": "mdi-book-open-variant",
					"nama":"LMS",
					"deskripsi":"Learning Mangement System untuk pegawai baru",
					"link":"lms",
					"link":"/apps/lms"
				},
			],
			miniVariant: false,
			right: true,
			rightDrawer: false,
			title: 'Si Bungkil'
		}
	}
}
</script>
<style>
.border--primary{
	border: 1px solid #FF6D00!important
}
</style>