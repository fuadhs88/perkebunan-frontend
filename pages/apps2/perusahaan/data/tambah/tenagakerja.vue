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
			title: "Tenaga Kerja",
			subtitle: "Kelola data Tenaga Kerja",
			headers: [
                    {
                        text: 'No',
                        value: 'proses',
                        form: false
                    }, 
                    {
                        text: 'Uraian',
                        value: 'tahun',
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'KWN Asing',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'KWN Indonesia',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Staf & Karyawan Bulanan',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Staf & Karyawan Harian Tetap',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Staf & Karyawan Harian Lepas',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Jumlah Pria',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Jumlah Wanita',
                        value: 'rencana',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                ],
            data:[]
        }
    }),
}
</script>