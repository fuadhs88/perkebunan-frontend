<template>
    <div>
        <Crud
			:crud="crud"/>
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan', 'triwulan'],
    watch:{
        triwulan: function(){
            this.crud.apiData               = `/v1/api/data/perusahaan_kendali_kebakaran/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`
            this.crud.headers[0].default    = this.triwulan
        }
    },
    data(){
        return {
            crud: {
                title: "Kendali Kebakaran",
                subtitle: "Kepemilikan Sarana Prasarana Sistem Cegah Dan Kendali Kebakaran",
                apiData: `/v1/api/data/perusahaan_kendali_kebakaran/id_perusahaan/${this.id_perusahaan}?field1=triwulan&value1=${this.triwulan}`,
                apiTambah: `/v1/api/tambah/perusahaan_kendali_kebakaran?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_kendali_kebakaran`,
                apiHapus: `/v1/api/hapus/perusahaan_kendali_kebakaran`,

                headers: [
                    { 
                        value: "triwulan",
                        default: this.triwulan,
                        type:'hidden',
                        table:false
                    }, 
                    {
                        text: 'Tipe',
                        value: 'tipe',
                        type:'radio',
                        options: [
                            {
                                label: 'Peralatan Utama',
                                value: 'Peralatan Utama',
                            },
                            {
                                label: 'Peralatan Pendukung',
                                value: 'Peralatan Pendukung',
                            },
                            {
                                label: 'Peralatan Diteksi Dini',
                                value: 'Peralatan Diteksi Dini',
                            },
                            {
                                label: 'Organisasi (Unit)',
                                value: 'Organisasi (Unit)',
                            },
                            {
                                label: 'SDM ( Orang )',
                                value: 'SDM ( Orang )',
                            },
                        ],
                    }, 
                    {
                        text: 'Jenis Sarana Prasarana & Sistem dimiliki',
                        value: 'jenis_sarana',
                        info: ['Contoh : Peralatan Tangan, Pompa Air Bertekanan Tinggi']
                    }, 
                    {
                        text: 'Jumlah',
                        value: 'jumlah',
                        type: 'number',
                        info: ['masukan satuan, Contoh : 1,2,3']
                    }, 
                    {
                        text: 'Keterangan',
                        value: 'keterangan',
                        type: 'textarea',
                        info: ['Contoh : 1 Regu 10 Personil, Lengkap, Baik']
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