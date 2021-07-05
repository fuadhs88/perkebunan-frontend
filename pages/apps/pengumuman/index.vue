<template>
	<div>
        <Head
            title="Pengumuman"
            subtitle="Pengumuman untuk perusahaan"
            color="text--black">
            <v-btn 
                v-if="tipe==='admin'"
                v-on:click="dialogForm=true" 
                small 
                class="d-xs-none">
                <v-icon left>mdi-plus-circle</v-icon>
                Tambah
            </v-btn>
        </Head>
        <v-alert
            v-if="data.length===0"
            border="left"
            close-text="Close Alert"
            color="deep-purple accent-4"
            dark>
            Belum ada pengumuman saat ini.
        </v-alert>
		<v-list 
            dense
            v-if="tipe==='admin'">
            <template
                v-for="(item, i) in data">
                <v-list-item
                    :key="`list-${i}`"
                    color="primary">
                    <v-list-item-icon>
                        <v-icon>mdi-bullhorn</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title v-text="item.judul"></v-list-item-title>
                        <v-list-item-subtitle v-text="item.deskripsi"></v-list-item-subtitle>
                    </v-list-item-content>
                    <v-list-item-action>
                        <v-row>
                        <v-btn icon v-on:click="handelEdit(item)">
                            <v-icon small>
                                mdi-pencil
                            </v-icon>
                        </v-btn>
                        <v-btn icon v-on:click="handleKonfirmasiHapus(item)">
                            <v-icon small>
                                mdi-delete
                            </v-icon>
                        </v-btn>
                        <v-btn 
                            icon
                            :to="`/apps/pengumuman/${item.id}`">
                            <v-icon
                                small
                                color="grey lighten-1">
                                mdi-chevron-right
                            </v-icon>
                        </v-btn>
                        </v-row>
                    </v-list-item-action>
                </v-list-item>
                <v-divider :key="i" />
            </template>
		</v-list>
        <v-list 
            dense
            v-else>
            <template
                v-for="(item, i) in data">
                <v-list-item
                    :key="`list-${i}`"
                    :to="`/apps/pengumuman/${item.id}`"
                    color="primary">
                    <v-list-item-icon>
                        <v-icon>mdi-bullhorn</v-icon>
                    </v-list-item-icon>
                    <v-list-item-content>
                        <v-list-item-title v-text="item.judul"></v-list-item-title>
                        <v-list-item-subtitle v-text="item.deskripsi"></v-list-item-subtitle>
                    </v-list-item-content>
                    <v-list-item-action>
                        
                        <v-icon
                            small
                            color="grey lighten-1">
                            mdi-chevron-right
                        </v-icon>
                        
                    </v-list-item-action>
                </v-list-item>
                <v-divider :key="i" />
            </template>
		</v-list>
        <!-- untuk form -->
		<v-dialog
            v-if="tipe==='admin'"
            v-model="dialogForm"
            max-width="500px">
            <v-card>
                <!-- untuk judul dipopup -->
                <v-card-title>
                    <span class="headline">Form Pengumuman</span>
                </v-card-title>

                <v-card-text>
                    <Form
                        :fields="fields"
                        :model="model"
                        :isFetching="isFetching"
                        :dialog="dialog"/>
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
                    v-on:click="handelSimpan">
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
	layout: 'apps2',
    data () {
		let tipe = this.$auth.$storage.getUniversal("loginType")
        return {
            tipe: tipe,
            dialogForm: false,
            dialogDelete: false,
            isFetching: false,
            dialog: {},
            data: [
                
            ],
            jalur:[],
            jalurTerpilih: 0,
            sekolahTerpilih: 0,
            model: {},
            crud: {
                apiData: `/v1/api/data/pengumuman`,
                apiTambah: `/v1/api/tambah/pengumuman`,
                apiUbah: `/v1/api/ubah/pengumuman`,
                apiHapus: `/v1/api/hapus/pengumuman`,
            },
            fields: [
                {
                    text: 'Judul',
                    value: 'judul',
                    info: ['Masukkan judul pengumuman']
                }, 
                {
                    text: 'Lampiran',
                    value: 'lampiran',
                    type: 'file',
                }, 
                {
                    text: 'Deskripsi',
                    value: 'deskripsi',
                    type: 'textarea',
                    info: ['Masukkan deskripsi pengumuman']
                }, 
            ]
        }
    },
    mounted(){ 
        this.handleUpdateData()
    },
	methods:{
        handleKonfirmasiHapus(item){
			// console.log(this)
            this.model          = Object.assign({}, item)
			this.dialogDelete	= true
		},
        handleUpdateData: async function (){
            let data = (await this.$api.$get(this.crud.apiData)).data
            this.data   = data
        },
        handelEdit: function(item){
            this.model      = Object.assign({}, item)
            this.dialogForm = true
        },
		handelSimpan: function(){
            this.isFetching = true
            let payload     = {}
            
            this.fields.filter((item)=>item.form!=false).map((item)=>{
                if(item.children===undefined){
                    payload[item.value]     = this.model[item.value]!=undefined?this.model[item.value]:''
                }else{
                    item.children.map((row)=>{
                        payload[row.value] = this.model[row.value]!=undefined?this.model[row.value]:''
                    })
                }
            })
            const api = this.model.id?`${this.crud.apiUbah}/${this.model.id}`:this.crud.apiTambah
			this.$api.$post(api, payload).then(async (resp)=>{
                this.isFetching = false
                this.dialog     = {
                    message: resp.message,
                    status: resp.status
                }
				if(resp.status){
                    this.dialogForm     = false
                    this.handleUpdateData()
                    this.model         = {}
                    // this.$nuxt.refresh()
				}
			})
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
                    // this.$nuxt.refresh()
				}
                
            })
            
			this.dialogDelete	= false
		},
	}
}
</script>
