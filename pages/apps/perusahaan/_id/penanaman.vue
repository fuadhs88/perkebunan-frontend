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
            this.crud.apiData               = `/v1/api/data/perusahaan_penanaman_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Penanaman",
                subtitle: "Kelola data Rencana Dan Realisasi Penanaman",
                apiData: `/v1/api/data/perusahaan_penanaman_lahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_penanaman_lahan?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_penanaman_lahan`,
                apiHapus: `/v1/api/hapus/perusahaan_penanaman_lahan`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    }, 
                    {
                        text: 'Tahun Penanaman',
                        value: 'tahun_penanaman',
                        type:'number',
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'Rencana HA',
                        value: 'rencana',
                        type:'number',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Inti (TBM)',
                        value: 'inti_tbm',
                        type:'number',
                    }, 
                    {
                        text: 'Inti (TM)',
                        value: 'inti_tm',
                        type:'number',
                    }, 
                    {
                        text: 'Plasma (TBM)',
                        value: 'plasma_tbm',
                        type:'number',
                    }, 
                    {
                        text: 'Plasma (TM)',
                        value: 'plasma_tm',
                        type:'number',
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        type: 'textarea',
                        table: false,
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