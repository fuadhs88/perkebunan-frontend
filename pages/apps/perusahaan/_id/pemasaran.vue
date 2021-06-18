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
        crud:{
            nested:true,
			title: "Pemasaran",
			subtitle: "Kelola Data Pemasaran",
            apiData: `/v1/api/data/perusahaan_pemasaran/id_perusahaan/${this.id_perusahaan}`,
            apiTambah: `/v1/api/tambah/perusahaan_pemasaran?id_perusahaan=${this.id_perusahaan}`,
            apiUbah: `/v1/api/ubah/perusahaan_pemasaran`,
            apiHapus: `/v1/api/hapus/perusahaan_pemasaran`,

			headers: [
                    {
                        text: 'Jenis Produksi',
                        value: 'jenis',
                        type:'radio',
                        options: [
                            {
                                label: 'TBS',
                                value: 'TBS',
                            },
                            {
                                label: 'Kernel',
                                value: 'Kernel',
                            },
                            {
                                label: 'CPO',
                                value: 'CPO',
                            },
                            {
                                label: 'PKO',
                                value: 'PKO',
                            },
                            {
                                label: 'PKE',
                                value: 'PKE',
                            },
                        ],
                        
                    }, 
                    {
                        text: 'Satuan',
                        value: 'satuan',
                        info: ['Contoh : Ton']
                    }, 
                    {
                        text: 'Dalam Negeri',
                        value: 'dalam_negeri',
                        align: "center",
                        children:[
                            {
                                text: 'Volume',
                                value: 'dn_volume',
                            },
                            {
                                text: 'Nilai',
                                value: 'dn_nilai',
                            },
                        ]
                    }, 
                    {
                        text: 'Ekspor',
                        value: 'ekspor',
                        align: "center",
                        children:[
                            {
                                text: 'Volume',
                                value: 'ekspor_volume',
                            },
                            {
                                text: 'Nilai',
                                value: 'ekspor_nilai',
                            },
                        ]
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