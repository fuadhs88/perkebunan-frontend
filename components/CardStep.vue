<template>
    <v-stepper v-model="instruksiAktif" vertical>
        <div v-for="(item, index) in instruksi" :key="index">
            <v-stepper-step :step="index+1" :complete="index+1<instruksiAktif">
                {{ item.judul }}
            </v-stepper-step>
            <v-stepper-content :step="index+1">
                <p>
                    <small>{{ item.instruksi }}</small>
                </p>
                <v-btn color="primary">
                    Ikuti
                </v-btn>
                <v-btn text @click="instruksiAktif += 1">
                    Selesai
                </v-btn>
            </v-stepper-content>
        </div>
    </v-stepper>
</template>
<script>
export default {
    props: ['instruksi', 'instruksiAktif', 'sm', 'md']
}
</script>