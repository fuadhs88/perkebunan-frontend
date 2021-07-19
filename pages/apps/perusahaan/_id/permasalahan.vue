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
            this.crud.apiData               = `/v1/api/data/perusahaan_permasalahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Permasalahan",
                subtitle: "Kelola data permasalahan yang dialami:",
                apiData: `/v1/api/data/perusahaan_permasalahan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_permasalahan?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_permasalahan`,
                apiHapus: `/v1/api/hapus/perusahaan_permasalahan`,

                headers: [
                        { 
                            value: "triwulan",
                            default: this.triwulan,
                            type:'hidden',
                            table:false
                        },        
                        {
                            text: 'Deskripsi',
                            value: 'deskripsi',
                            type: 'textarea',
                            info: ['Masukkan deskripsi permasalahan'],
                        },                 
                        {
                            text: 'Lampiran',
                            value: 'lampiran',
                            type: 'file',
                            info: ['Sertakan lampiran'],
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