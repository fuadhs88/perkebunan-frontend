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
			title: "HAT",
			subtitle: "Penyelesaian Hak Atas Tanah",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Proses',
                        value: 'proses',
                        info: ['Contoh : Pembebasan Lahan (dari kawasan hutan)']
                    }, 
                    {
                        text: 'Triwulan Lalu',
                        value: 'proses',
                        info: ['Contoh : satuan dalam HA'],
                    }, 
                    {
                        text: 'Triwulan Ini',
                        value: 'proses',
                    }, 
                    {
                        text: 'S/D Saat ini',
                        value: 'proses',
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