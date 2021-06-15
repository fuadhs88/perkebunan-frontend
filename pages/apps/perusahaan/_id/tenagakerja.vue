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
                title: "Tenaga Kerja",
                subtitle: "Kelola data Tenaga Kerja",
                apiData: `/v1/api/data/perusahaan_tenaga_kerja/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_tenaga_kerja?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_tenaga_kerja`,
                apiHapus: `/v1/api/hapus/perusahaan_tenaga_kerja`,

                headers: [
                    {
                        text: 'Tipe',
                        value: 'tipe',
                        type:'radio',
                        options: [
                            {
                                label: 'Kantor Direksi',
                                value: 'Kantor Direksi',
                            },
                            {
                                label: 'Kantor Kebun',
                                value: 'Kantor Kebun',
                            },
                            {
                                label: 'Karyawan Lapangan',
                                value: 'Karyawan Lapangan',
                            },
                            {
                                label: 'Pabrik',
                                value: 'Pabrik',
                            }
                        ],
                        info: ['masukkan tahun, Contoh : 2020, 2021']
                    }, 
                    {
                        text: 'Uraian',
                        value: 'uraian',
                        info: ['masukkan jabatan, Contoh : General Manager, Manager Kebun']
                    }, 
                    {
                        text: 'KWN Asing',
                        value: 'kewarganegaraan_asing',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'KWN Indonesia',
                        value: 'kewarganegaraan_indonesia',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'S&K Karyawan Bulanan',
                        value: 'sk_bulanan',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'S&K Harian Tetap',
                        value: 'sk_harian_tetap',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'S&K Harian Lepas',
                        value: 'sk_harian_lepas',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Jumlah Pria',
                        value: 'jenis_kelamin_p',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
                    }, 
                    {
                        text: 'Jumlah Wanita',
                        value: 'jenis_kelamin_w',
                        type: 'number',
                        info: ['satuan (orang), Contoh : 20'],
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