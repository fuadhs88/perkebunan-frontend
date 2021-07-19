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
            this.crud.apiData               = `/v1/api/data/perusahaan_lahan_gambut/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Lahan Gambut",
                subtitle: "Kelola data Lahan Gambut",
                apiData: `/v1/api/data/perusahaan_lahan_gambut/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_lahan_gambut?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_lahan_gambut`,
                apiHapus: `/v1/api/hapus/perusahaan_lahan_gambut`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    }, 
                    {
                        text: 'Lahat Gambut',
                        value: 'lahan_gambut',
                        info: ['masukkan Lahan Gambut']
                    }, 
                    {
                        text: 'Kondisi',
                        value: 'kondisi',
                        info: ['masukkan Kondisi']
                    }, 
                    {
                        text: 'Luasan',
                        value: 'luasan',
                        type:'number',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Koordinat',
                        value: 'koordinat',
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