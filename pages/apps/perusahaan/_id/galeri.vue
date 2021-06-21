<template>
    <div>
        <Head
            title="Galeri"
            subtitle="Kelola galeri perusahaan"
            color="black--text">
            <v-btn 
                small
                v-on:click="dialogForm=true">
                <v-icon left>
                    mdi-image-plus
                </v-icon>
                Tambah Galeri
            </v-btn>
        </Head>
        <v-alert 
            v-if="data.length===0"
            type="info" 
            border="left">
            <div class="title">Oops ... </div>
            belum ada galeri di perusahaan ini
        </v-alert>
        <v-row
            v-else>
            <v-col
                v-for="card in data"
                :key="card.judul"
                cols="12" 
                md="4">
            <v-card>
            <v-img
                :src="`${api_url}/${card.url}`"
                class="white--text align-end d-flex"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
                >
                <v-app-bar
                    flat
                    color="rgba(0, 0, 0, 0)"
                >
                    <v-toolbar-title class="text-overline white--text pl-0">
                    {{card.judul}}
                    </v-toolbar-title>

                    <v-spacer></v-spacer>

                    <v-btn
                        color="white"
                        icon
                        v-on:click="handleKonfirmasiHapus(card)">
                    <v-icon>mdi-image-remove</v-icon>
                    </v-btn>
                    <v-btn 
                        color="white" 
                        icon 
                        target="_blank"
                        :href="`${api_url}/${card.url}`">
                        <v-icon>mdi-launch</v-icon>
                    </v-btn>
                </v-app-bar>
            </v-img>
            </v-card>
            </v-col>
        </v-row>

        <!-- untuk popup form dan edit -->
        <v-dialog
            v-model="dialogForm"
            max-width="500px"
        >
            <v-card>
                <!-- untuk judul dipopup -->
                <v-card-title>
                    <span class="headline">Tambah Galeri</span>
                </v-card-title>

                <v-card-text>
                    <v-container v-if="crud.nested===undefined">
                        <Form
                            :fields="crud.headers"
                            :model="model"
                            :isFetching="isFetching"
                            :dialog="dialog"/>
                    </v-container>
                    <v-container v-else>
                        <Form
                            :fields="crud.headers.filter((item)=>item.children===undefined)"
                            :model="model"
                            :isFetching="isFetching"
                            :dialog="dialog"/>
                        <div
                            v-for="(item, index) in crud.headers.filter((item)=>item.children!=undefined)"
                            :key="index">
                            <p class="subtitle-3 mb-0">{{item.text}}</p>
                            <Form
                                class="ml-6 mb-6"
                                :fields="item.children"
                                :model="model"/>
                        </div>
                    </v-container>
                </v-card-text>
                
                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="dialogForm=false">
                    Batal
                </v-btn>
                <v-btn
                    color="blue darken-1"
                    text
                    v-on:click="handleSimpan">
                    Simpan
                </v-btn>
                </v-card-actions>
            </v-card>
        </v-dialog>

        <!-- untuk popup konfirmasi delete -->
		<v-dialog v-model="dialogDelete" max-width="500px">
			<v-card>
				<v-card-title class="headline">Apakah anda yakin ingin menghapus data ini ?</v-card-title>
				<v-card-actions>
				<v-spacer></v-spacer>
				<v-btn color="blue darken-1" text @click="dialogDelete=false">Batal</v-btn>
				
				<v-btn color="blue darken-1" text @click="handleHapus">OK</v-btn>
				<v-spacer></v-spacer>
				</v-card-actions>
			</v-card>
		</v-dialog>
		
    </div>
</template>
<script>
export default {
    props: ['id_perusahaan'],
    data(){
        return {
            api_url: process.env.API_URL,
            model: {

            },
            dialogForm: false,
            dialogDelete: false,
            isFetching:false,
            dialog: {},
            crud: {
                nested:true,
                title: "Produksi",
                subtitle: "Kelola Data Produksi",
                apiData: `/v1/api/data/perusahaan_galeri/id_perusahaan/${this.id_perusahaan}`,
                apiTambah: `/v1/api/tambah/perusahaan_galeri?id_perusahaan=${this.id_perusahaan}`,
                apiUbah: `/v1/api/ubah/perusahaan_galeri`,
                apiHapus: `/v1/api/hapus/perusahaan_galeri`,
                headers: [
                    {
                        text: 'Judul',
                        value: 'judul',
                    }, 
                    {
                        text: 'File',
                        value: 'url',
                        type: 'file',
                    }, 
                ],
            },
            data: [],
        }
    },
    mounted: function(){
        this.handleUpdateData()
    },
    methods: {
        handleKonfirmasiHapus(item){
			// console.log(this)
            this.model        = Object.assign({}, item)
			this.dialogDelete	= true
		},
        handleHapus(){
            this.isFetching     = true
            this.$api.$get(`${this.crud.apiHapus}/${this.model.id}`).then((resp)=>{
                this.isFetching     = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
                if(resp.status){
                    this.dialogDelete	= false
                    this.handleUpdateData()
                    this.model  = {}
                    // this.$nuxt.refresh()
				}
                
            })
            
			this.dialogDelete	= false
		},
        handleSimpan(){
            this.isFetching = true
            let payload     = this.model
            
			this.$api.$post(this.crud.apiTambah, payload).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    this.dialogForm     = false
                    this.handleUpdateData()
                    this.model  = {}
                    // this.$nuxt.refresh()
				}
			})
        },
        handleUpdateData: async function (){
            let data = (await this.$api.$get(this.crud.apiData)).data
            this.data   = data
        },
    }
}
</script>