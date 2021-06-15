<template>
    <div>
        <p class="subtitle-2">LEGALITAS YANG DIPEROLEH :</p>
        <p class="subtitle-3 mb-0">a. Ijin Lokasi</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasi"
            :model="model"
            :isFetching="isFetching"
            :dialog="dialog"/>
        <p class="subtitle-3 mb-0">b. PPUB/ IUP</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsPPUB"
            :model="model"/>
        <p class="subtitle-3 mb-0">c. IPL</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIPL"
            :model="model"/>
        <div class="text-right">
            <v-btn 
                v-on:click="handleSimpan"
                type="submit"
                color="primary">
                Simpan
            </v-btn>
        </div>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan'],
    mounted: function(){
        this.handleUpdateData()
    },
    data(){
        return {
            isFetching: false,
            dialog: {},
            model: {},
            apiData: `/v1/api/detil/perusahaan_legalitas/${this.id_perusahaan}/id_perusahaan`,
            apiUbah: `/v1/api/ubah/perusahaan_legalitas/`,
            apiTambah: `/v1/api/tambah/perusahaan_legalitas`,
            fieldsLokasi:[
                {
                    text: 'Nomor',
                    value: 'lokasi_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021']
                }, 
                {
                    text: 'Tanggal',
                    value: 'lokasi_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'lokasi_luas',
                    type: 'number',
                    info: ['Contoh :  4.100, Hektar'],
                }, 
            ],
            fieldsPPUB:[
                {
                    text: 'Nomor',
                    value: 'ppub_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021']
                }, 
                {
                    text: 'Tanggal',
                    value: 'ppub_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ppub_luas',
                    type: 'number',
                    info: ['Contoh :  4.100, Hektar'],
                }, 
            ],
            fieldsIPL:[
                {
                    text: 'Nomor',
                    value: 'ipl_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021']
                }, 
                {
                    text: 'Tanggal',
                    value: 'ipl_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ipl_luas',
                    type: 'number',
                    info: ['Contoh :  4.100, Hektar'],
                }, 
            ]
        }
    },
    methods:{
        handleUpdateData: async function(){
            const model         = (await this.$api.$get(this.apiData)).data
            this.model          = model || {
                id_perusahaan:this.id_perusahaan
            }
        },
        handleSimpan: function(){
			this.isFetching = true
            const api = this.model.id?`${this.apiUbah}${this.model.id}`:this.apiTambah
			this.$api.$post(api, this.model).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    this.dialogForm     = false
                    this.handleUpdateData()
                    // this.$nuxt.refresh()
				}
			})
		}
    }
}
</script>