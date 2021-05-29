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
			title: "Kemitraan Lainnya",
			subtitle: "Kelola Data Kerjasama Kemitraan Lainnya",
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
                        text: 'Jenis Keigatan',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'Volumen Kegiatan',
                        value: 'no_mou',
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'no_mou',
                    }, 
                ],
            data:[]
        }
    }),
}
</script>