<template>
    <div>
        <Crud
			:crud="crud"
            color="text--black"/>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan'],
    data(){
        return {
            crud: {
                nested:true,
                title: "Produksi",
                subtitle: "Kelola Data Produksi",
                apiData: `/v1/api/data/perusahaan_produksi/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_produksi?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_produksi`,
                apiHapus: `/v1/api/hapus/perusahaan_produksi`,

                headers: [
                    {
                        text: 'Tahun',
                        value: 'tahun',
                        info: ['Contoh : 2021, 2022']
                    }, 
                    {
                        text: 'Triwulan',
                        value: 'triwulan',
                        type:'radio',
                        options: [
                            {
                                label: 'TR. I',
                                value: 'TR. I',
                            },
                            {
                                label: 'TR. 2',
                                value: 'TR. 2',
                            },
                            {
                                label: 'TR. 3',
                                value: 'TR. 3',
                            },
                            {
                                label: 'TR. 4',
                                value: 'TR. 4',
                            },
                        ],
                        info: ['Contoh : 1, 2, 3']
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