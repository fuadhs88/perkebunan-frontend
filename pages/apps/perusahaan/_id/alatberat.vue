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
            this.crud.apiData               = `/v1/api/data/perusahaan_alat_berat/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Alat Berat",
                subtitle: "Kelola data Jumlah Dan Jenis Alat Berat yang digunakan",
			
                apiData: `/v1/api/data/perusahaan_alat_berat/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_alat_berat?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_alat_berat`,
                apiHapus: `/v1/api/hapus/perusahaan_alat_berat`,

                headers: [             
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    },        
                    {
                        text: 'Jenis',
                        value: 'jenis',
                        info: ['Contoh : Traktor, Buldozer, Exavator, dll']
                    }, 
                    {
                        text: 'Jumlah Unit',
                        value: 'jumlah',
                        type: 'number',
                        info: ['Contoh : 1, 2, 3, ']
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        info: ['Contoh : Baik, Sangat Baik']
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