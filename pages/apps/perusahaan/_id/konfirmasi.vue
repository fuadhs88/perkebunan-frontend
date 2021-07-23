<template>
	<div>
        <div class="d-flex" style="height:100vh;">
		<v-col class="mx-auto my-auto" sm="12" md="6" cols="12">
            <v-card 
                v-if="tipe==='perusahaan'"
                class="border--primary">
                <v-card-title class="pb-0">
                    Konfirmasi
                </v-card-title>
                <v-card-text>
                    <div>Apakah semua informasi sudah benar ?</div>
                </v-card-text>
                <v-card-actions>
                    <v-spacer></v-spacer>
                    <v-btn 
                        v-on:click="handelSimpan('selesai')"
                        :class="model[`triwulan${triwulan.substr(4,1)}`]==='selesai'?'primary':''">
                        Sudah
                        <v-icon right dark>mdi-check-all</v-icon>
                    </v-btn>
                    <v-btn 
                        v-on:click="handelSimpan('belum')"
                        :class="model[`triwulan${triwulan.substr(4,1)}`]!='selesai' || model[triwulan.substr(4,1)]===null?'primary':''">
                        Belum
                        <v-icon right dark>mdi-radiobox-blank</v-icon>
                    </v-btn>
                </v-card-actions>
            </v-card>
            <v-card 
                v-else
                class="border--primary">
                <div v-if="model.selesai==='selesai' || model.selesai==='terima'">
                    <v-card-title class="pb-0">
                        Konfirmasi
                    </v-card-title>
                    <v-card-text>
                        <div>Terbitkan bukti serah terima ?</div>
                    </v-card-text>
                    <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn 
                            v-on:click="handelSimpan('terima')"
                            :class="model.selesai==='terima'?'primary':''">
                            Terbitkan
                            <v-icon right dark>mdi-check-all</v-icon>
                        </v-btn>
                        <v-btn 
                            v-on:click="handelSimpan('selesai')"
                            :class="model.selesai==='selesai'?'primary':''">
                            Belum
                            <v-icon right dark>mdi-radiobox-blank</v-icon>
                        </v-btn>
                    </v-card-actions>
                </div>
                <div v-else>
                    <v-card-title class="pb-0">
                        Oops
                    </v-card-title>
                    <v-card-text>
                        <div>Perusahaan belum mengkonfirmasi data sesuai</div>
                    </v-card-text>
                </div>
                
            </v-card>
        </v-col>
        </div>
        
		<v-dialog
			v-model="isFetching"
			hide-overlay
			persistent
			width="300"
			>
			<v-card
				color="primary"
				dark
			>
				<v-card-text>
				Menyimpan ...
				<v-progress-linear
					indeterminate
					color="white"
					class="mb-0"
				></v-progress-linear>
				</v-card-text>
			</v-card>
		</v-dialog>
        <v-dialog
            v-if="dialog"
			v-model="modal"            
			width="300">
			<v-alert
                v-model="modal"
                border="top"
                color="green accent-4"
                dark
                dismissible
                type="success"
                >
                {{ dialog.message }}
            </v-alert>
		</v-dialog>
	</div>
</template>
<script>
export default {
    props: ['id_perusahaan', 'triwulan'],
    // watch:{
    //     triwulan: function(){
    //         this.crud.apiData               = `/v1/api/detil/perusahaan_triwulan/${this.id_perusahaan}/id_perusahaan?field1=tahun&value1=${this.triwulan.substr(0,4)}`
    //     }
    // },
    mounted: function(){
        this.handleUpdateData()
    },
    data () {
		let tipe = this.$auth.$storage.getUniversal("loginType")
        return {
            tipe: tipe,
            dialogForm: false,
            dialogDelete: false,
            isFetching: false,
            dialog: {},
            modal:false,
            data: [
                
            ],
            jalur:[],
            jalurTerpilih: 0,
            sekolahTerpilih: 0,
            model: {},
            crud: {
                apiData: `/v1/api/detil/perusahaan_triwulan/${this.id_perusahaan}/id_perusahaan?field1=tahun&value1=${this.triwulan.substr(0,4)}`,
                apiUbah: `/v1/api/perusahaanTriwulanUpdate/${this.id_perusahaan}`,
            },
            fields: [
                {
                    text: 'Judul',
                    value: 'judul',
                    info: ['Masukkan judul pengumuman']
                }, 
                {
                    text: 'Lampiran',
                    value: 'lampiran',
                    type: 'file',
                }, 
                {
                    text: 'Deskripsi',
                    value: 'deskripsi',
                    type: 'textarea',
                    info: ['Masukkan deskripsi pengumuman']
                }, 
            ]
        }
    },
	methods:{
        handleKonfirmasiHapus(item){
			// console.log(this)
            this.model          = Object.assign({}, item)
			this.dialogDelete	= true
		},
        handleUpdateData: async function (){
            const model         = (await this.$api.$get(this.crud.apiData)).data || {}
            this.model          = model
        },
        handelEdit: function(item){
            this.model      = Object.assign({}, item)
            this.dialogForm = true
        },
		handelSimpan: function(selesai){
            this.isFetching = true
            let payload     = {
                tahun:this.triwulan.substr(0,4),
                triwulan:`triwulan${this.triwulan.substr(4,1)}`,
                status: selesai
            }

            const api = `${this.crud.apiUbah}`
			this.$api.$post(api, payload).then(async (resp)=>{
                this.isFetching = false
                this.modal      = true;
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    this.dialogForm     = false
                    this.handleUpdateData()
                    this.model         = {}
                    // this.$nuxt.refresh()
				}
			})
        },
        
	}
}
</script>
