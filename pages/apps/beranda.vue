<template>
	<div>
		<Head
			title="Si Bungkil"
			subtitle="Sistem Informasi Pembangunan Perkebunan Berkelanjutan"
			color="text--black"/>
		<v-row class="mt-2">
			<v-col v-for="(item, index) in apps" :key="index" sm="12" md="3" cols="12">
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
	props: ['apps'],
	data: () => ({
		
    }),
	methods:{
		
	}
}
</script>
