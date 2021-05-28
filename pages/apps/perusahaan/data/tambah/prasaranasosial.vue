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
			title: "Prasarana Sosial",
			subtitle: "Kelola data Sarana dan Prasarana Sosial kemasyarakatan",
			headers: [
                    {
                        text: 'No',
                        value: 'no',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Sarana/Prasarana',
                        value: 'jenis',
                        info: ['Contoh : Sarana Ibadah, Sarana Pendidikan']
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