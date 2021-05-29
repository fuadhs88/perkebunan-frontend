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
			subtitle: "Kelola data lahan pembibitan",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Kegiatan',
                        value: 'proses',
                        info: ['Contoh : BENIH, SP2B, Realisasi Benih, Pre Nursery'],
                    }, 
                    {
                        text: 'Luas (HA)',
                        value: 'proses',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Jumlah Bibit (Btg)',
                        value: 'proses',
                        info: ['Contoh : satuan dalam Btg'],
                        
                    }, 
                    {
                        text: 'Umur (Bln)',
                        value: 'proses',
                        info: ['Contoh : satuan dalam Bln'],
                        
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