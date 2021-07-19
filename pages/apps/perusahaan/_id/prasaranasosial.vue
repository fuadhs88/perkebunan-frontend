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
            this.crud.apiData               = `/v1/api/data/perusahaan_prasarana_sosial/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Prasarana Sosial",
                subtitle: "Kelola data Sarana dan Prasarana Sosial kemasyarakatan",
			
                apiData: `/v1/api/data/perusahaan_prasarana_sosial/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_prasarana_sosial?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_prasarana_sosial`,
                apiHapus: `/v1/api/hapus/perusahaan_prasarana_sosial`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    },        
                    {
                        text: 'Sarana/Prasarana',
                        value: 'nama_sarana',
                        info: ['Contoh : Sarana Ibadah, Sarana Pendidikan']
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
                        type: 'textarea',
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