<template>
    <div>
        <p class="subtitle-2">LEGALITAS YANG DIPEROLEH :</p>

        <p class="subtitle-3">a. Ijin Lokasi</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasi"
            :model="model"
            :isFetching="isFetching"
            :dialog="dialog"/>

        <p class="subtitle-3">b. Ijin Lokasi Perpanjangan 1</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasiPerpanjangan1"
            :model="model"/>

        <p class="subtitle-3">c. Ijin Lokasi Perpanjangan 2</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasiPerpanjangan2"
            :model="model"/>

        <p class="subtitle-3">d. Ijin Lokasi Perpanjangan 3</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsLokasiPerpanjangan3"
            :model="model"/>

        <p class="subtitle-3">e. IUP/PPUB</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsPPUB"
            :model="model"/>

        <p class="subtitle-3">f. IPL</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIPL"
            :model="model"/>

        <p class="subtitle-3">g. Perpanjangan IPL</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIPLPerpanjangan"
            :model="model"/>
        
        <p class="subtitle-3">h. IPL Tahap II</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIPL2"
            :model="model"/>
        
        <p class="subtitle-3">i. IPL Tahap III</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIPL3"
            :model="model"/>

        <p class="subtitle-3">j. Izin Prinsip Pelepasan Hutan</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsIzinPelepasanHutan"
            :model="model"/>

        <p class="subtitle-3">k. SK Pelepasan Hutan</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsSKPelepasanHutan"
            :model="model"/>

        <p class="subtitle-3">l. HGU</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsHGU"
            :model="model"/>
        
        <p class="subtitle-3">m. HGB</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsHGB"
            :model="model"/>

        <p class="subtitle-3">n. SK Amdal/UKL/UPL</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsSKAmdal"
            :model="model"/>

        <p class="subtitle-3">o. SK Ruang Plasma</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsSKRuangPlasma"
            :model="model"/>

        <p class="subtitle-3">p. SK CPP</p>
        <Form
            class="ml-6 mb-6"
            :fields="fieldsSKCPP"
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
    props: ['id_perusahaan', 'triwulan'],
    mounted: function(){
        this.handleUpdateData()
    },
    watch:{
        triwulan: function(){
            this.handleUpdateData()
        }
    },
    data(){
        return {
            isFetching: false,
            dialog: {},
            model: {},
            apiData: ``,
            apiUbah: `/v1/api/ubah/perusahaan_legalitas/`,
            apiTambah: `/v1/api/tambah/perusahaan_legalitas?id_perusahaan=${this.id_perusahaan}`,
            fieldsLokasi:[
                {
                    text: 'Nomor',
                    value: 'lokasi_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'lokasi_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'lokasi_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsLokasiPerpanjangan1:[
                {
                    text: 'Nomor',
                    value: 'lokasi_perpanjangan1_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'lokasi_perpanjangan1_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'lokasi_perpanjangan1_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsLokasiPerpanjangan2:[
                {
                    text: 'Nomor',
                    value: 'lokasi_perpanjangan2_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'lokasi_perpanjangan2_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'lokasi_perpanjangan2_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsLokasiPerpanjangan3:[
                {
                    text: 'Nomor',
                    value: 'lokasi_perpanjangan3_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'lokasi_perpanjangan3_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'lokasi_perpanjangan3_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsPPUB:[
                {
                    text: 'Nomor',
                    value: 'ppub_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'ppub_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ppub_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsIPL:[
                {
                    text: 'Nomor',
                    value: 'ipl_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'ipl_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ipl_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsIPLPerpanjangan:[
                {
                    text: 'Nomor',
                    value: 'ipl_perpanjangan_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'ipl_perpanjangan_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ipl_perpanjangan_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsIPL2:[
                {
                    text: 'Nomor',
                    value: 'ipl2_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'ipl2_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ipl2_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsIPL3:[
                {
                    text: 'Nomor',
                    value: 'ipl3_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'ipl3_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'ipl3_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsIzinPelepasanHutan:[
                {
                    text: 'Nomor',
                    value: 'izin_pelepasan_hutan_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'izin_pelepasan_hutan_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
            ],
            fieldsSKPelepasanHutan:[
                {
                    text: 'Nomor',
                    value: 'sk_pelepasan_hutan_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'sk_pelepasan_hutan_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
            ],
            fieldsHGU:[
                {
                    text: 'Nomor',
                    value: 'hgu_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'hgu_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'hgu_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsHGB:[
                {
                    text: 'Nomor',
                    value: 'hgb_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'hgb_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
                {
                    text: 'Luas (satuan ha)',
                    value: 'hgb_luas',
                    type: 'number',
                    info: ['Contoh :  4100, Hektar'],
                    md:2,
                }, 
            ],
            fieldsSKAmdal:[
                {
                    text: 'Nomor',
                    value: 'sk_amdal_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'sk_amdal_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
            ],
            fieldsSKRuangPlasma:[
                {
                    text: 'Nomor',
                    value: 'sk_ruang_plasma_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'sk_ruang_plasma_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
            ],
            fieldsSKCPP:[
                {
                    text: 'Nomor',
                    value: 'sk_cpp_nomor',
                    info: ['Contoh : XXX/XX/HK/XI/2021'],
                    md:7,
                }, 
                {
                    text: 'Tanggal',
                    value: 'sk_cpp_tanggal',
                    type: 'date',
                    info: ['Contoh : 14 Nopember 2014'],
                    md:3,
                }, 
            ],
        }
    },
    methods:{
        handleUpdateData: async function(){
            this.apiData        = `/v1/api/detil/perusahaan_legalitas/${this.id_perusahaan}/id_perusahaan?field1=triwulan&value1=${this.triwulan}`
            const model         = (await this.$api.$get(this.apiData)).data
            this.model          = model || {
                id_perusahaan:this.id_perusahaan,
                triwulan: this.triwulan
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