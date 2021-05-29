<template>
	<div>
		<Head
			title="SIBUNGKIL"
			subtitle="Sistem Informasi Perkebunan Dengan Teknologi Unggulan"
			color="text--black"/>
		<v-row class="mt-6">
			
			<v-col v-for="(item, index) in apps" :key="index" sm="12" md="3">
				<v-card class="border--primary">
					<v-card-title class="pb-0">
						<v-icon left>{{item.ikon}}</v-icon>
						{{item.nama}}
					</v-card-title>
					<v-card-text>
						<div>{{item.deskripsi}}</div>
					</v-card-text>
					<v-card-actions>
						<v-spacer></v-spacer>
						<v-btn color="primary" text :to="item.link">
							Buka
							<v-icon right dark>mdi-launch</v-icon>
						</v-btn>
					</v-card-actions>
				</v-card>
			</v-col>
		</v-row>
		
	</div>
</template>
<script>
export default {
	layout:'apps2',
	params: ['apps'],
	data: () => ({
		apps:[
			{
				"ikon": "mdi-domain",
				"nama":"Perusahaan",
				"deskripsi":"Sistem Pengelolaan informasi perusahaan",
				"link":"apps2/perusahaan"
			},
			{
				"ikon": "mdi-cash-multiple",
				"nama":"Keuangan",
				"deskripsi":"Sistem Pengelolaan Data Keuangan Terpadu",
				"link":"apps2/keuangan"
			},
			{
				"ikon": "mdi-account-tie",
				"nama":"Kepegawaian",
				"deskripsi":"Sistem Pengelolaan Data Kepegawaian Terpadu",
				"link":"apps2/kepegawaian"
			},
			{
				"ikon": "mdi-calendar-clock",
				"nama":"Kehadiran",
				"deskripsi":"Sistem Pengelolaan Data Kehadiran Terpadu",
				"link":"ppdb",
				"link":"apps2/kehadiran"
			},
			{
				"ikon": "mdi-book-open-variant",
				"nama":"LMS",
				"deskripsi":"Learning Mangement System untuk pegawai baru",
				"link":"lms",
				"link":"apps2/kehadiran"
			},
		],
    }),
	methods:{
		
	}
}
</script>
