<template>
    <div>
        <Head 
			title="Cetak" 
			subtitle="Overview sebelum dicetak"
            color="text--black"
			>
			<div>
				<v-btn 
					v-on:click="handelCetak"
					small>
					<v-icon left>mdi-printer-check</v-icon>
					Cetak Sekarang
				</v-btn>
			</div>
		</Head>
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
            <section slot="pdf-content" style="padding:30px;font-family: 'Times New Roman';">
                <!-- start -->
                <div class="text-center">
                    <div style="padding:30px">
                        <v-img
                            src="/logo-print.png"/>
                    </div>
                    <h2>DEPARTEMEN PERTANIAN</h2>
                    <br/>
                    <h3>
                        LAPORAN KEMAJUAN KEGIATAN <br/>
                        PERUSAHAAN PERKEBUNAN <br/>
                        TRIWULAN-II<br/>
                        TAHUN 2020
                    </h3>
                    
                </div>
                <div class="html2pdf__page-break"/>
                <div style="margin-top:32px"/>
                <h4 class="text-center">
                    LAPORAN KEMAJUAN KEGIATAN PERUSAHAAN PERKEBUNAN PERIODE LAPORAN: TRIWULAN- II ( April – Juni 2020 )
                </h4>
                <br/>
                <p>
                    <strong>Data Perusahaan :</strong>
                </p>
                <table style="border-collapse: collapse; ">
                    <tbody>
                        <tr>
                            <td width="30px">1. </td>
                            <td width="200px">Nama Perusahaan</td>
                            <td>: {{ perusahaan.nama }}</td>
                        </tr>
                        <tr>
                            <td>2. </td>
                            <td>NPWP</td>
                            <td>: {{ perusahaan.npwp }}</td>
                        </tr>
                        <tr>
                            <td>3. </td>
                            <td>Status Perusahaan</td>
                            <td>: {{ perusahaan.status_perusahaan }}</td>
                        </tr>
                        <tr>
                            <td>4. </td>
                            <td>Alamat</td>
                            <td></td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>a. &nbsp; Kantor Pusat</td>
                            <td>: {{ perusahaan.alamat_kantor_pusat }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>b. &nbsp; Kantor Pusat</td>
                            <td>: {{ perusahaan.alamat_kantor_cabang }}</td>
                        </tr>
                        <tr>
                            <td>5. </td>
                            <td>Nama Kebun/ Estate</td>
                            <td>: {{ perusahaan.nama_kebun }}</td>
                        </tr>
                        <tr>
                            <td>6. </td>
                            <td>Lokasi Kebun/ Pabrik</td>
                            <td></td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>a. &nbsp; Desa</td>
                            <td>: {{ perusahaan.lokasi_kebun_desa }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>b. &nbsp; Kecamatan</td>
                            <td>: {{ perusahaan.lokasi_kebun_kecamatan }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>c. &nbsp; Kabupaten</td>
                            <td>: {{ perusahaan.lokasi_kebun_kabupaten }}</td>
                        </tr>
                        <tr>
                            <td></td>
                            <td>d. &nbsp; Provinsi</td>
                            <td>: {{ perusahaan.lokasi_kebun_provinsi }}</td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                <p>
                    <strong>LEGALITAS YANG DIPEROLEH</strong>
                </p>
                <p>1. SuratPersetujuan/Perijinan yang diperoleh :</p>
                <p>a. Ijin Lokasi</p>
                <table style="border-collapse: collapse; margin-left:32px">
                    <tbody>
                        <tr>
                            <td width="147">Nomor </td>
                            <td>: {{ legalitas.lokasi_nomor }} </td>
                        </tr>
                        <tr>
                            <td>Tanggal </td>
                            <td>: {{ legalitas.lokasi_tanggal }} </td>
                        </tr>
                        <tr>
                            <td>Luas </td>
                            <td>: {{ legalitas.lokasi_luas }} ha</td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                <p>b. PPUB/ IUP</p>
                <table style="border-collapse: collapse; margin-left:32px">
                    <tbody>
                        <tr>
                            <td width="147">Nomor </td>
                            <td>: {{ legalitas.ppub_nomor}} </td>
                        </tr>
                        <tr>
                            <td>Tanggal </td>
                            <td>: {{ legalitas.ppub_tanggal}} </td>
                        </tr>
                        <tr>
                            <td>Luas </td>
                            <td>: {{ legalitas.ppub_luas}} ha</td>
                        </tr>
                    </tbody>
                </table>
                <br/>
                <p>b. IPL<p/>
                <table style="border-collapse: collapse; margin-left:32px">
                    <tbody>
                        <tr>
                            <td width="147">Nomor </td>
                            <td>: {{ legalitas.ipl_nomor}} </td>
                        </tr>
                        <tr>
                            <td>Tanggal </td>
                            <td>: {{ legalitas.ipl_tanggal}} </td>
                        </tr>
                        <tr>
                            <td>Luas </td>
                            <td>: {{ legalitas.ipl_luas}} ha</td>
                        </tr>
                    </tbody>
                </table>
                <div class="html2pdf__page-break"/>
                <div style="margin-top:32px"/>
                <br/>
                <p>
                    <strong>1. Lahan Pembibitan</strong>
                </p>
                <table style="border-collapse: collapse; width: 100%;">
                    <tbody>
                        <tr>
                            <td width="36">
                                <p>No</p>
                            </td>
                            <td width="186">
                                <p>Kegiatan</p>
                            </td>
                            <td width="83">
                                <p>Luas ( HA )</p>
                            </td>
                            <td width="96">
                                <p>JumlahBibit ( Btg)</p>
                            </td>
                            <td width="115">
                                <p>Umur ( Bln )</p>
                            </td>
                            <td width="101">
                                <p>Keterangan</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>1</p>
                            </td>
                            <td width="186">
                                <p>BENIH</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>a. SP2B</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>b. Realisasi Benih</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>2</p>
                            </td>
                            <td width="186">
                                <p>BIBITAN</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>a.&nbsp;&nbsp; Pre Nursery</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>b. Main Nursery</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>c.&nbsp;&nbsp; BIBIT</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td width="36">
                                <p>&nbsp;</p>
                            </td>
                            <td width="186">
                                <p>&nbsp;</p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                        <tr>
                            <td colspan="2" width="222">
                                <p><strong><em>Total</em></strong></p>
                            </td>
                            <td width="83">
                                <p>&nbsp;</p>
                            </td>
                            <td width="96">
                                <p>&nbsp;</p>
                            </td>
                            <td width="115">
                                <p>&nbsp;</p>
                            </td>
                            <td width="101">
                                <p>&nbsp;</p>
                            </td>
                        </tr>
                    </tbody>
                </table>
                <!-- end of -->
            </section>
            
        </vue-html2pdf>
    </div>
</template>
<script>
import VueHtml2pdf from 'vue-html2pdf'
export default {
    components: {
        VueHtml2pdf
    },
    async asyncData({ params, $api }){
        const id_perusahaan = params.id
        const perusahaan    = (await $api.$get(`/v1/api/detil/perusahaan/${id_perusahaan}`)).data
        const legalitas     = (await $api.$get(`/v1/api/detil/perusahaan_legalitas/${id_perusahaan}`)).data
		return {
			id_perusahaan,
            perusahaan,
            legalitas,
		}
	},
    data: () => ({
        
    }),
    methods:{
		handelCetak(){
			this.$refs.html2Pdf.generatePdf()
		},
    }
}
</script>
<style scoped>
.text-center{
    text-align:center
}
p{
    margin-bottom:8px;
}
</style>