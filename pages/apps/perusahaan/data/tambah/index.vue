<template>
    <div>
        <p class="subtitle-2">DATA PERUSAHAAN :</p>
        <Form
            :fields="fields"/>
        <div class="text-right">
            <v-btn 
                type="submit"
                color="primary">
                Simpan
            </v-btn>
        </div>
    </div>
</template>
<script>
export default {
    data: () => ({
    fields:[
        {
            text: 'Nama Perusahaan',
            value: 'proses',
            info: ['Contoh : PT. Perkebunan Nusantara']
        }, 
        {
            text: 'NPWP',
            value: 'proses',
            info: ['Contoh : 123XXXXXXX'],
        }, 
        {
            text: 'Status Perusahaan',
            value: 'proses',
        }, 
        {
            text: 'Kantor Pusat',
            value: 'proses',
            info: ['Contoh : Alamanda Tower XX Jl.TB.Simatupang Kav.XX Cilandak Barat.'],
        }, 
        {
            text: 'Kantor Cabang',
            value: 'proses',
            info: ['Contoh : Samarinda'],
        }, 
        {
            text: 'Nama Kebun/ Estate',
            value: 'proses',
            info: ['Contoh : Karangan Estate'],
        }, 
        {
            text: 'Nama Kebun/ Estate',
            value: 'proses',
            info: ['Contoh : Karangan Estate'],
        }, 
        {
            text: 'Desa',
            value: 'proses',
            info: ['Contoh : Desa'],
        }, 
        {
            text: 'Desa',
            value: 'proses',
            info: ['Contoh : Batu Lepoq'],
        }, 
        {
            text: 'Kecamatan',
            value: 'proses',
            info: ['Contoh : Batu Lepoq'],
        }, 
        {
            text: 'Kabupaten',
            value: 'proses',
            info: ['Contoh : Kutai Timur'],
        }, 
        {
            text: 'Provinsi',
            value: 'proses',
            info: ['Contoh : Kalimantan Timur'],
        }, 
    ]
    }),
}
</script>