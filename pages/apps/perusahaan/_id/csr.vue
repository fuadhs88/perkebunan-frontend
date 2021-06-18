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
                title: "CSR",
                subtitle: "PROGRAM COMMUNITY DEVELOPMENT/CORPORATE SOCIAL RESPONSIBILITY",
                apiData: `/v1/api/data/perusahaan_csr/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_csr?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_csr`,
                apiHapus: `/v1/api/hapus/perusahaan_csr`,

                headers: [
                        {
                            text: 'Deskripsi',
                            value: 'deskripsi',
                            type: 'textarea',
                            info: ['Masukkan deskripsi csr'],
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