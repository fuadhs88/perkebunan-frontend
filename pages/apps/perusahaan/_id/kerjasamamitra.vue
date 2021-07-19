<template>
    <div>
        <Crud
			:crud="crud"
            color="text--black"/>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan', 'triwulan'],
    watch:{
        triwulan: function(){
            this.crud.apiData               = `/v1/api/data/perusahaan_kerjasama_kemitraan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
        crud:{
            nested:true,
			title: "Kerjasama Kemitraan",
			subtitle: "Kelola Data Kerjasama Kemitraan",
            apiData: `/v1/api/data/perusahaan_kerjasama_kemitraan/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
            apiTambah: `/v1/api/tambah/perusahaan_kerjasama_kemitraan?id_perusahaan=${this.id_perusahaan}`,
            apiUbah: `/v1/api/ubah/perusahaan_kerjasama_kemitraan`,
            apiHapus: `/v1/api/hapus/perusahaan_kerjasama_kemitraan`,

			headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    },        
                    {
                        text: 'Nama Koperasi',
                        value: 'nama_koperasi',
                    }, 
                    {
                        text: 'No MOU',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'Tanggal MOU',
                        value: 'tanggal_mou',
                        type: 'date',
                    }, 
                    {
                        text: 'target',
                        value: 'target',
                        align: "center",
                        children:[
                            {
                                text: 'KK',
                                value: 'target_kk',
                                type: 'number',
                            },
                            {
                                text: 'Luas (Ha)',
                                value: 'target_luas',
                                type: 'number',
                            },
                        ]
                    }, 
                    {
                        text: 'Realisasi',
                        value: 'realisasi',
                        align: "center",
                        children:[
                            {
                                text: 'KK',
                                value: 'realisasi_kk',
                                type: 'number',
                            },
                            {
                                text: 'TBM',
                                value: 'realisasi_luas_tbm',
                                type: 'number',
                            },
                            {
                                text: 'TM',
                                value: 'realisasi_luas_tm',
                                type: 'number',
                            },
                        ]
                    }, 
                    {
                        text: 'Tahun Tanam',
                        value: 'tahun_tanam',
                        type: 'number',
                    }, 
                    {
                        text: 'Aksi',
                        value: 'aksi',
                        align: "center",
                        form: false
                    }
                ],
            data:[]
            }
        }
    }
}
</script>