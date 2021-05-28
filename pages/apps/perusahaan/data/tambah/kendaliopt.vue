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
                        info: ['Contoh : A, B, C']
                    }, 
                    {
                        text: 'Jenis Sarana Prasarana dan Sistem Yang dimiliki',
                        value: 'tahun',
                        info: ['Contoh : Peralatan Pengamatan, Menara api']
                    }, 
                    {
                        text: 'Jumlah',
                        value: 'rencana',
                        info: ['masukan satuan, Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        info: ['Contoh : Lengkap, Baik']
                    }, 
                ],
            data:[]
        }
    }),
}
</script>