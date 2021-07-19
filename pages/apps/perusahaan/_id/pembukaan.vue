<template>
    <div>
        <Crud
			:crud="crud"/>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan', 'triwulan'],
    watch:{
        triwulan: function(){
            this.crud.apiData               = `/v1/api/data/perusahaan_pembukaan_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Lahan",
                subtitle: "Kelola data Rencana Dan Realisasi Pembukaan Lahan",
                apiData: `/v1/api/data/perusahaan_pembukaan_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_pembukaan_lahan?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_pembukaan_lahan`,
                apiHapus: `/v1/api/hapus/perusahaan_pembukaan_lahan`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    }, 
                    {
                        text: 'Tahun LC',
                        value: 'tahun_lc',
                        type: 'number',
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'Rencana HA',
                        value: 'rencana',
                        type: 'number',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Realisasi Inti',
                        value: 'realisasi_inti',
                        type: 'number',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Realisasi Plasma',
                        value: 'realisasi_plasma',
                        type: 'number',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        type: 'textarea',
                    }, 
                    {
                        text: 'Aksi',
                        value: 'aksi',
                        form: false
                    }
                ],
            },
            data:[]
        }
    },
}
</script>