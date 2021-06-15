<template>
    <div>
        <Crud
			:crud="crud"/>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan'],
    data(){
        return {
            crud: {
                title: "Sarana Produksi",
                subtitle: "Kelola data sarana produksi",
                apiData: `/v1/api/data/perusahaan_sarana_produksi/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_sarana_produksi?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_sarana_produksi`,
                apiHapus: `/v1/api/hapus/perusahaan_sarana_produksi`,

                headers: [
                    {
                        text: 'Jenis',
                        value: 'jenis',
                        info: ['masukkan jenis, Contoh : Pupuk, Agro Chemical']
                    }, 
                    {
                        text: 'Satuan',
                        value: 'satuan',
                        info: ['Contoh : Kg, Ltr'],
                    }, 
                    {
                        text: 'Jumlah',
                        value: 'jumlah',
                        type: 'number',
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        type: 'textarea',
                        table: false,
                    }, 
                    {
                        text: 'Aksi',
                        value: 'aksi',
                        form: false
                    }
                ],
            },
            data:[]
        }
    },
}
</script>