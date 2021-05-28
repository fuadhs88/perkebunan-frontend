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
			title: "Kendali OPT",
			subtitle: "Kepemilikan Sarana Prasarana Sistem Cegah dan Kendali OPT",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        info: ['Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Jenis',
                        value: 'tahun',
                        info: ['Contoh : Pupuk, Agro Chemical']
                    }, 
                    {
                        text: 'Satuan',
                        value: 'rencana',
                        info: ['Contoh : Kg, Ltr']
                    }, 
                    {
                        text: 'Jumlah',
                        value: 'rencana',
                        info: ['masukan format angka Contoh : 10, 20, 30']
                    }, 
                    {
                        text: 'Keterangan/ Perincian',
                        value: 'keterangan',
                    }, 
                ],
            data:[]
        }
    }),
}
</script>