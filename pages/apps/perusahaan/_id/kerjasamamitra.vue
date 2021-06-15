<template>
    <div>
        <Crud
			:crud="crud"
            color="text--black"/>
    </div>
</template>
<script>
export default {
    data: () => ({
        crud:{
            nested:true,
			title: "Kerjasama Kemitraan",
			subtitle: "Kelola Data Kerjasama Kemitraan",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Nama Koperasi',
                        value: 'nama_koperasi',
                    }, 
                    {
                        text: 'No dan Tgl MOU',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'target',
                        value: 'target',
                        align: "center",
                        children:[
                            {
                                text: 'KK',
                                value: 'target_kk',
                            },
                            {
                                text: 'Luas (Ha)',
                                value: 'target_luas',
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
                            },
                            {
                                text: 'TBM',
                                value: 'realisasi_tbm',
                            },
                            {
                                text: 'TM',
                                value: 'realisasi_tm',
                            },
                        ]
                    }, 
                    {
                        text: 'Tahun Tanam',
                        value: 'tahun_tanam',
                    }, 
                ],
            data:[]
        }
    }),
}
</script>