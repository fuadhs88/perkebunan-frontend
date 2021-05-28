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
			title: "Kendali Kebakaran",
			subtitle: "Kepemilikan Sarana Prasarana Sistem Cegah Dan Kendali Kebakaran",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        info: ['Contoh : A, B, C']
                    }, 
                    {
                        text: 'Jenis Sarana Prasarana dan Sistem Yang dimiliki',
                        value: 'tahun',
                        info: ['Contoh : Peralatan Tangan, Pompa Air Bertekanan Tinggi']
                    }, 
                    {
                        text: 'Jumlah',
                        value: 'rencana',
                        info: ['masukan satuan, Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        info: ['Contoh : 1 Regu 10 Personil, Lengkap, Baik']
                    }, 
                ],
            data:[]
        }
    }),
}
</script>