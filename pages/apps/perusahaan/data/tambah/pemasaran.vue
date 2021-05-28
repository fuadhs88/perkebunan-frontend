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
			title: "Pemasaran",
			subtitle: "Kelola Data Pemasaran",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Jenis Produksi',
                        value: 'jenis_produksi',
                        info: ['Contoh : TBS, Kernel, CPO']
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
                                value: 'dalam_negeri_volume',
                            },
                            {
                                text: 'Nilai',
                                value: 'dalam_negeri_nilai',
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
                ],
            data:[]
        }
    }),
}
</script>