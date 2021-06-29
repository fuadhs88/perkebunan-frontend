<template>
	<div>
        <Head
            :title="detil.judul"
            :subtitle="$moment(detil.dibuat).format('DD MMM, HH:mm')"
            color="text--black"/>
        <v-btn
            v-if="detil.lampiran!=''"
            :href="detil.lampiran"
            target="_blank">
            Buka Lampiran
            <v-icon right>
                mdi-launch
            </v-icon>
        </v-btn>
        <div class="mt-4">
            {{detil.deskripsi}}
        </div>
        
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
