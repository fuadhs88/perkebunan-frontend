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
                title: "Lahan",
                subtitle: "Kelola data lahan pembibitan",
                apiData: `/v1/api/data/perusahaan_lahan_pembibitan/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_lahan_pembibitan?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_lahan_pembibitan`,
                apiHapus: `/v1/api/hapus/perusahaan_lahan_pembibitan`,

                headers: [
                        {
                            text: 'Tipe',
                            value: 'tipe',
                            type:'radio',
                            options: [
                                {
                                    label: 'BIBIT',
                                    value: 'BIBIT',
                                },
                                {
                                    label: 'BIBITAN',
                                    value: 'BIBITAN',
                                }
                            ],
                            info: ['Contoh : BENIH, BIBITAN'],
                        }, 
                        {
                            text: 'Kegiatan',
                            value: 'kegiatan',
                            info: ['Contoh : BENIH, SP2B, Realisasi Benih, Pre Nursery'],
                        }, 
                        {
                            text: 'Luas (HA)',
                            value: 'luas',
                            type: 'number',
                            info: ['Contoh : satuan dalam HA'],
                        }, 
                        {
                            text: 'Jumlah Bibit (Btg)',
                            value: 'jumlah_bibit',
                            type: 'number',
                            info: ['Contoh : satuan dalam Btg'],
                            
                        }, 
                        {
                            text: 'Umur (Bln)',
                            value: 'umur',
                            type: 'number',
                            info: ['Contoh : satuan dalam Bln'],
                            
                        }, 
                        {
                            text: 'Keterangan',
                            type: 'textarea',
                            value: 'keterangan',
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