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
                title: "Kendali OPT",
                subtitle: "Kepemilikan Sarana Prasarana Sistem Cegah dan Kendali OPT",
                apiData: `/v1/api/data/perusahaan_kendali_opt/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_kendali_opt?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_kendali_opt`,
                apiHapus: `/v1/api/hapus/perusahaan_kendali_opt`,

                headers: [
                    {
                        text: 'Tipe',
                        value: 'tipe',
                        type:'radio',
                        options: [
                            {
                                label: 'Peralatan Pengamatan',
                                value: 'Peralatan Pengamatan',
                            },
                            {
                                label: 'Peralatan Pengendalian',
                                value: 'Peralatan Pengendalian',
                            },
                            {
                                label: 'Peralatan Pelindung Diri',
                                value: 'Peralatan Pelindung Diri',
                            },
                            {
                                label: 'Organisasi',
                                value: 'Organisasi',
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
                        info: ['Contoh : Menara Api, Mobil Patroli, Master']
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