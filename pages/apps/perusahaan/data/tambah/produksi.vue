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
			title: "Produksi",
			subtitle: "Kelola Data Produksi",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
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
                                text: 'Ton CBS',
                                value: 'inti_cbs',
                            },
                            {
                                text: 'Kernel',
                                value: 'inti_kernel',
                            },
                            {
                                text: 'CPO',
                                value: 'inti_cpo',
                            },
                            {
                                text: 'PKO',
                                value: 'inti_pko',
                            },
                            {
                                text: 'PKE',
                                value: 'inti_pke',
                            },
                        ]
                    }, 
                    {
                        text: 'Plasma',
                        value: 'plasma',
                        align: "center",
                        children:[
                            {
                                text: 'Ton CBS',
                                value: 'plasma_inti',
                            },
                            {
                                text: 'Kernel',
                                value: 'plasma_kernel',
                            },
                            {
                                text: 'CPO',
                                value: 'plasma_cpo',
                            },
                            {
                                text: 'PKO',
                                value: 'plasma_pko',
                            },
                            {
                                text: 'PKE',
                                value: 'plasma_pke',
                            },
                        ]
                    }, 
                ],
            data:[]
        }
    }),
}
</script>