<template>
	<div>
		<Header title="SIBUNGKIL"/>
		<v-row class="mt-6">
			<v-col v-for="(item, index) in apps" :key="index" sm="12" md="3">
				<v-card>
					<v-card-title class="pb-0">{{item.nama}}</v-card-title>
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
	layout:'apps',
	data: () => ({
		apps:[
			{
				"nama":"Perusahaan",
				"deskripsi":"Sistem Pengelolaan informasi perusahaan",
				"link":"apps/perusahaan"
			},
			{
				"nama":"Keuangan",
				"deskripsi":"Sistem Pengelolaan Data Keuangan Terpadu",
				"link":"apps/keuangan"
			},
			{
				"nama":"Kepegawaian",
				"deskripsi":"Sistem Pengelolaan Data Kepegawaian Terpadu",
				"link":"apps/kepegawaian"
			},
			{
				"nama":"Kehadiran",
				"deskripsi":"Sistem Pengelolaan Data Kehadiran Terpadu",
				"link":"ppdb",
				"link":"apps/kehadiran"
			},
			{
				"nama":"LMS",
				"deskripsi":"Learning Mangement System untuk pegawai baru",
				"link":"lms",
				"link":"apps/kehadiran"
			},
		]
    }),
	methods:{
		
	}
}
</script>
