<template>
    <div>
        <p class="subtitle-2">DATA PERUSAHAAN :</p>
        <Form
            class="ml-6 mb-6"
            :fields="fields"
            :model="model"
            :isFetching="isFetching"
            :dialog="dialog"/>
        <p class="subtitle-3 mt-4">Lokasi Kebun / Pabrik</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasiKebun"
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
            apiData: `/v1/api/detil/perusahaan/${this.id_perusahaan}`,
            apiUbah: `/v1/api/ubah/perusahaan/${this.id_perusahaan}`,
            apiTambah: `/v1/api/tambah/perusahaan`,

            fields:[
                {
                    text: 'Nama Perusahaan',
                    value: 'nama',
                    info: ['Contoh : PT. Perkebunan Nusantara']
                }, 
                {
                    text: 'Email Pengelola',
                    value: 'email_pengelola',
                    info: ['Contoh : PT. Perkebunan Nusantara']
                }, 
                {
                    text: 'NPWP',
                    value: 'npwp',
                    info: ['Contoh : 123XXXXXXX'],
                }, 
                {
                    text: 'Status Perusahaan',
                    value: 'status_perusahaan',
                }, 
                {
                    text: 'Kantor Pusat',
                    value: 'alamat_kantor_pusat',
                    info: ['Contoh : Alamanda Tower XX Jl.TB.Simatupang Kav.XX Cilandak Barat.'],
                }, 
                {
                    text: 'Kantor Cabang',
                    value: 'alamat_kantor_cabang',
                    info: ['Contoh : Samarinda'],
                }, 
                {
                    text: 'Nama Kebun/ Estate',
                    value: 'nama_kebun',
                    info: ['Contoh : Karangan Estate'],
                }, 
            ],
            fieldsLokasiKebun: [
                {
                    text: 'Desa',
                    value: 'lokasi_kebun_desa',
                    info: ['Contoh : Desa cimahi selatan'],
                }, 
                {
                    text: 'Kecamatan',
                    value: 'lokasi_kebun_kecamatan',
                    info: ['Contoh : Batu Lepoq'],
                }, 
                {
                    text: 'Kabupaten',
                    value: 'lokasi_kebun_kabupaten',
                    info: ['Contoh : Kutai Timur'],
                }, 
                {
                    text: 'Provinsi',
                    value: 'lokasi_kebun_provinsi',
                    info: ['Contoh : Kalimantan Timur'],
                }, 
                {
                    text: 'Posisi latitude Kebun',
                    value: 'lokasi_kebun_lat',
                    info: ['Contoh : 0.1409258'],
                }, 
                {
                    text: 'Posisi latitude Kebun',
                    value: 'lokasi_kebun_lng',
                    info: ['Contoh : 117.4908734'],
                }, 
            ]
        }
    },
    methods:{
        handleUpdateData: async function(){
            const model         = (await this.$api.$get(this.apiData)).data
            this.model          = model
        },
        handleSimpan: function(){
			this.isFetching = true
            const api = this.model.id?this.apiUbah:this.apiTambah
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