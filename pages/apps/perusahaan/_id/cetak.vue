<template>
    <div>
        <Head 
			title="Cetak" 
			subtitle="Overview sebelum dicetak"
            color="text--black"
			>
			<div>
				<!-- <v-btn 
					v-on:click="handelCetak"
					small>
					<v-icon left>mdi-printer-check</v-icon>
					Cetak Sekarang
				</v-btn> -->
			</div>
		</Head>
        <iframe src="/laporan.pdf" style="border:none; width:100%; height:800px"/>
        <!-- <vue-html2pdf
            :show-layout="true"
            :float-layout="false"
            :enable-download="true"
            :preview-modal="true"
            filename="print perusahaan"
            :paginate-elements-by-height="1100"
            :pdf-quality="2"
            pdf-format="a4"
            pdf-orientation="portrait"
            pdf-content-width="800px"
            :manual-pagination="false"
            ref="html2Pdf">
            <section slot="pdf-content">
                <div style="text-align:center; padding:12px">
                    <h1>DEPARTEMEN PERTANIAN</h1>
                </div>
            </section>
        </vue-html2pdf> -->
    </div>
</template>
<script>
import VueHtml2pdf from 'vue-html2pdf'
export default {
    components: {
        VueHtml2pdf
    },
    data: () => ({
        crud:{
			title: "Kemitraan Lainnya",
			subtitle: "Kelola Data Kerjasama Kemitraan Lainnya",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Nama Koperasi',
                        value: 'nama_koperasi',
                    }, 
                    {
                        text: 'Jenis Keigatan',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'Volumen Kegiatan',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'no_mou',
                    }, 
                ],
            data:[]
        }
    }),
    methods:{
		handelCetak(){
			this.$refs.html2Pdf.generatePdf()
		},
    }
}
</script>