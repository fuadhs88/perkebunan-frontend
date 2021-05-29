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
			title: "Pembangunan Pabrik",
			subtitle: "Kelola data Rencana Dan Realisasi Pembangunan Pabrik",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Uraian',
                        value: 'tahun',
                        info: ['Contoh : Jumlah (Unit), Kapasitas Ijin, Kapasitas Terpasang']
                    }, 
                    {
                        text: 'Rencana',
                        value: 'rencana',
                    }, 
                    {
                        text: 'Realisasi',
                        value: 'inti_tbm',
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