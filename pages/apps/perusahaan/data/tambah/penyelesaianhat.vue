<template>
    <div>
        <p class="subtitle-2">DATA PERUSAHAAN :</p>
        <v-form ref="form">
            <v-text-field
                label="Nama Proses"
                :messages="['Contoh : Penerimaan Siswa Baru Tahun 2021']"/>
            <div class="text-right">
                <v-btn 
                    type="submit"
                    color="primary">
                    Simpan
                </v-btn>
            </div>
        </v-form>
    </div>
</template>