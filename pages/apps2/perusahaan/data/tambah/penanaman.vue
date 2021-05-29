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
			title: "Penanaman",
			subtitle: "Kelola data Rencana Dan Realisasi Penanaman",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Tahun Penanaman',
                        value: 'tahun',
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'Rencana HA',
                        value: 'rencana',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Inti (TBM)',
                        value: 'inti_tbm',
                    }, 
                    {
                        text: 'Inti (TM)',
                        value: 'inti_tm',
                    }, 
                    {
                        text: 'Plasma (TBM)',
                        value: 'plasma_tbm',
                    }, 
                    {
                        text: 'Plasma (TM)',
                        value: 'plasma_tm',
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                    }, 
                ],
            data:[]
        }
    }),
}
</script>