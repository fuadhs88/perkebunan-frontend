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
            this.crud.apiData               = `/v1/api/data/perusahaan_produksi/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                nested:true,
                title: "Produksi",
                subtitle: "Kelola Data Produksi",
                apiData: `/v1/api/data/perusahaan_produksi/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_produksi?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_produksi`,
                apiHapus: `/v1/api/hapus/perusahaan_produksi`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    },        
                    {
                        text: 'Tahun',
                        value: 'tahun',
                        info: ['Contoh : 2021, 2022']
                    }, 
                    {
                        text: 'Inti',
                        value: 'inti',
                        align: "center",
                        children:[
                            {
                                text: 'Ton TBS',
                                value: 'inti_tbs',
                                type:'number'
                            },
                            {
                                text: 'Kernel',
                                value: 'inti_kernel',
                                type:'number'
                            },
                            {
                                text: 'CPO',
                                value: 'inti_cpo',
                                type:'number'
                            },
                            {
                                text: 'PKO',
                                value: 'inti_pko',
                                type:'number'
                            },
                            {
                                text: 'PKE',
                                value: 'inti_pke',
                                type:'number'
                            },
                        ]
                    }, 
                    {
                        text: 'Plasma',
                        value: 'plasma',
                        align: "center",
                        children:[
                            {
                                text: 'Ton TBS',
                                value: 'plasma_tbs',
                                type:'number'
                            },
                            {
                                text: 'Kernel',
                                value: 'plasma_kernel',
                                type:'number'
                            },
                            {
                                text: 'CPO',
                                value: 'plasma_cpo',
                                type:'number'
                            },
                            {
                                text: 'PKO',
                                value: 'plasma_pko',
                                type:'number'
                            },
                            {
                                text: 'PKE',
                                value: 'plasma_pke',
                                type:'number'
                            },
                        ]
                    }, 
                    {
                        text: 'Aksi',
                        value: 'aksi',
                        form: false
                    }
                ],
            data:[]
            }
        }
    }
}
</script>