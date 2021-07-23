<template>
	<div>
        <div class="d-flex" style="height:100vh;" v-if="model[`triwulan${triwulan.substr(4,1)}`]!='selesai'">
            <v-col class="mx-auto my-auto" sm="12" md="6" cols="12">
                <v-card class="border--primary">
                    <v-card-title class="pb-0">
                        Oops
                    </v-card-title>
                    <v-card-text>
                        <div>Admin belum mengkonfirmasi data perusahaan</div>
                    </v-card-text>
                </v-card>
            </v-col>
        </div>
        <div v-else>
            <div class="text-right">
                <v-btn 
                    v-on:click="handelCetak"
                    small>
                    <v-icon left>mdi-printer-check</v-icon>
                    Cetak / Export PDF
                </v-btn>
                
            </div>
            <vue-html2pdf
                :show-layout="true"
                :float-layout="false"
                :enable-download="false"
                :preview-modal="true"
                filename="print perusahaan"
                :paginate-elements-by-height="1100"
                :pdf-quality="2"
                
                pdf-format="a4"
                pdf-orientation="portrait"
                pdf-content-width="800px"
                :manual-pagination="false"
                ref="html2Pdf">
                <section slot="pdf-content" style="font-family:Times New Roman; padding:20px">
                    <v-img
                        style="position:absolute"
                        width="80px"
                        src="/kutai.png"/>
                    <div style="text-align:center; padding:12px;">
                        <p style="font-size:16pt; margin:0">PEMERINTAH KABUPATEN KUTAI TIMUR</p>
                        <p style="font-size:24pt; margin:0">DINAS PERKEBUNAN</p>
                        <p style="font-size:10pt; margin:0">Pusat Pemerintahan Bukit Pelangi Telp./Fax. (0549) 22981 E-mail : disbunkutim@plasa.com</p>
                        <p style="font-size:16pt; margin:0">S A N G A T T A</p>
                    </div>
                    <hr/>
                    <hr/>
                    <br/>
                    <br/>
                    <p style="font-size:16pt; text-align:center">TANDA TERIMA LAPORAN</p>
                    <br/>
                    <br/>
                    <p style="font-size:12pt">Telah diterima Laporan Progres Pembangunan Perkebunan Melalui Sistem Informasi Pembangunan Perkebunan ( Si Bungkil) dari:</p>
                    
                    <ol>
                        <li style="line-height: 150%; margin: 0cm 0cm 0cm 0px; font-size: 12pt; ">Nama Perusahaan &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : {{ model.nama }}</li>
                        <li style="line-height: 150%; margin: 0cm 0cm 0cm 0px; font-size: 12pt; ">Waktu &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : {{ $moment(model.diubah).format('DD MMM YYYY, HH:mm:ss') }}</li>
                    </ol>
                    <br/>
                    <p style="font-size:12pt; ">Demikian tanda terima ini dikeluarkan untuk dapat dipergunan sebagaimana mestinya.</p>
                    <br/>
                    
                    <table style="width:100%; text-align:center">
                        <tr>
                            <td width="50%">
                                Barcode<br/>
                                <vue-qrcode :value="`nama%20perusahaan:${model.nama}`" />
                            </td>
                            <td>
                                ttd
                                <br/>
                                <br/>
                                <br/>
                                Dinas Perkebunan
                            </td>
                        </tr>
                    </table>
                </section>
            </vue-html2pdf>
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
import VueHtml2pdf from 'vue-html2pdf'
import VueQrcode from 'vue-qrcode'
export default {
    components: {
        VueHtml2pdf,
        VueQrcode
    },
    props: ['id_perusahaan', 'triwulan'],
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
                apiUbah: `/v1/api/ubah/perusahaan/${this.id_perusahaan}`,
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
        handelCetak(){
			this.$refs.html2Pdf.generatePdf()
		},
        handleKonfirmasiHapus(item){
			// console.log(this)
            this.model          = Object.assign({}, item)
			this.dialogDelete	= true
		},
        handleUpdateData: async function (){
            const model         = (await this.$api.$get(this.crud.apiData)).data
            console.log(model)
            this.model          = model
        },
        handelEdit: function(item){
            this.model      = Object.assign({}, item)
            this.dialogForm = true
        },
		handelSimpan: function(selesai){
            this.isFetching = true
            let payload     = {
                selesai
            }

            const api = `${this.crud.apiUbah}/${this.model.id}`
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
