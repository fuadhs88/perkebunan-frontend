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
                nested: true,
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
                        align: "center",
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
                        align: "center",
                        info: ['masukkan jabatan, Contoh : General Manager, Manager Kebun']
                    }, 
                    {
                        text: 'Kewarganegaraan',
                        value: 'uraian',
                        align: "center",
                        children: [
                            {
                                text: 'Asing',
                                value: 'kewarganegaraan_asing',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                            {
                                text: 'Indonesia',
                                value: 'kewarganegaraan_indonesia',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                        ],
                    }, 
                    {
                        text: 'Staff & Karyawan',
                        value: 'uraian',
                        align: "center",
                        children: [
                            {
                                text: 'Bulanan',
                                value: 'sk_bulanan',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                            {
                                text: 'H. Tetap',
                                value: 'sk_harian_tetap',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                            {
                                text: 'H. Lepas',
                                value: 'sk_harian_lepas',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                        ],
                    }, 
                    {
                        text: 'Kelamin',
                        value: 'uraian',
                        align: "center",
                        children: [
                            {
                                text: 'L',
                                value: 'jenis_kelamin_p',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                            {
                                text: 'P',
                                value: 'jenis_kelamin_w',
                                type: 'number',
                                info: ['satuan (orang), Contoh : 20'],
                            }, 
                        ],
                    }, 
                    
                    {
                        text: 'Aksi',
                        value: 'aksi',
                        align: "center",
                        form: false
                    }
                ],
            },
            data:[]
        }
    },
}
</script>