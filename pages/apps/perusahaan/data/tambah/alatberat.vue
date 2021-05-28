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
			title: "Alat Berat",
			subtitle: "Kelola data Jumlah Dan JenisAlat Berat yang digunakan",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Jenis',
                        value: 'jenis',
                        info: ['Contoh : Traktor, Buldozer, Exavator, dll']
                    }, 
                    {
                        text: 'Jumlah Unit',
                        value: 'jumlah_unit',
                        info: ['Contoh : 1, 2, 3, ']
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        info: ['Contoh : Baik, Sangat Baik']
                    }, 
                ],
            data:[]
        }
    }),
}
</script>