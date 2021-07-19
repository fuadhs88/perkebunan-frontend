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
            this.crud.apiData               = `/v1/api/data/perusahaan_kemitraan_lainnya/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Kemitraan Lainnya",
                subtitle: "Kelola Data Kerjasama Kemitraan Lainnya",
                apiData: `/v1/api/data/perusahaan_kemitraan_lainnya/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_kemitraan_lainnya?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_kemitraan_lainnya`,
                apiHapus: `/v1/api/hapus/perusahaan_kemitraan_lainnya`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    },        
                    {
                        text: 'Jenis Koperasi',
                        value: 'jenis_koperasi',
                    }, 
                    {
                        text: 'Jenis Keigatan',
                        value: 'jenis_kegiatan',
                    }, 
                    {
                        text: 'Volume Kegiatan',
                        value: 'volume_kegiatan',
                    }, 
                    {
                        text: 'Keterangan',
                        type: 'textarea',
                        value: 'keterangan',
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