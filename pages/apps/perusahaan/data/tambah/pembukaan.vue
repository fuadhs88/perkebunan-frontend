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
			title: "Lahan",
			subtitle: "Kelola data Rencana Dan Realisasi Pembukaan Lahan",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Tahun LC',
                        value: 'tahun',
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'Rencana HA',
                        value: 'rencana',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Realisasi Inti',
                        value: 'realisasi_inti',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Realisasi Plasma',
                        value: 'realisasi_plasma',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'proses',
                    }, 
                ],
            data:[]
        }
    }),
}
</script>