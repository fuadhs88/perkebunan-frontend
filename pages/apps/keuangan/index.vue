<template>
	<div class="d-flex justify-center">
		<!-- <Head 
			class="mx-auto my-auto text-center"
			title="Opps" 
			subtitle="Modul ini belum tersedia"
			color="text--black"/> -->
			<v-alert type="error" border="left">
				<div class="title">Oops ... </div>
				Modul ini belum tersedia
			</v-alert>
	</div>
</template>
<script>
export default {
	layout:'apps2',
	data: ()=>({
		
	}),
	methods:{
		
	}
}
</script>