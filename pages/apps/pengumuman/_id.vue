<template>
	<div>
        <Head
            :title="detil.judul"
            :subtitle="$moment(detil.dibuat).format('DD MMM, HH:mm')"
            color="text--black"/>
        {{detil.deskripsi}}
	</div>
</template>
<script>
export default {
	layout: 'apps2',
	data: () => ({        
		detil: {}
    }),
    mounted(){ 
        this.handleUpdateData()
    },
	methods:{
        handleUpdateData: async function (){
            let id      = this.$route.params.id
            let detil   = (await this.$api.$get(`/v1/api/detil/pengumuman/${id}`)).data
            this.detil  = detil
        },	
	}
}
</script>
