<template>
    <div>
        <p class="subtitle-2">LEGALITAS YANG DIPEROLEH :</p>
        <p class="subtitle-3 mb-0">a. Ijin Lokasi</p>
        <Form
            class="ml-6 mb-6"
            :fields="fields"/>
        <p class="subtitle-3 mb-0">b. PPUB/ IUP</p>
        <Form
            class="ml-6 mb-6"
            :fields="fields"/>
        <p class="subtitle-3 mb-0">c. IPL</p>
        <Form
            class="ml-6 mb-6"
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
            text: 'Nomor',
            value: 'proses',
            info: ['Contoh : XXX/XX/HK/XI/2021']
        }, 
        {
            text: 'Tanggal',
            value: 'proses',
            info: ['Contoh : 14 Nopember 2014'],
        }, 
        {
            text: 'Luas',
            value: 'proses',
            info: ['Contoh :  4.100, Hektar'],
        }, 
    ]
    }),
}
</script>