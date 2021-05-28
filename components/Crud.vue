<template>
	<div>
        <!-- untuk header -->
		<Head 
			:title="crud.title" 
			:subtitle="crud.subtitle"
			:handleDelete="dipilih.length>0 && handleKonfirmasiHapus"
            :color="color">
            <v-btn small
                v-on:click="handleOpenFormTambah">
                <v-icon left>mdi-plus-circle</v-icon>
                Tambah
            </v-btn>
        </Head>
        <!-- untuk table -->
		<v-data-table
			dense
			v-model="dipilih"
			:headers="crud.headers"
            :hide-default-header="crud.nested"
			:items="crud.data||data"
			item-key="name"
			show-select
			class="elevation-1"
			height="65vh">
            
            <template
                v-if="crud.nested"
                v-slot:header="{ props: {headers} }">
                <thead>
                <template v-for="item in [processTableHeaders(headers)]">
                    <tr :key="item.value">
                        <th v-for="header in item.parents"
                            :key="header.value"
                            :rowspan="header.rowspan"
                            :colspan="header.colspan"
                            :width="header.width"
                            :class="header.align ? `text-${header.align}` : ''"
                            style="border: thin solid rgba(0, 0, 0, 0.12)">
                            {{ header.text }}
                        </th>
                    </tr>
                    <tr v-if="item.children"
                        :key="item.value">
                        <th v-for="header in item.children"
                            :key="header.value"
                            :width="header.width"
                            :class="header.align ? `text-xs-${header.align}` : ''"
                            style="border: thin solid rgba(0, 0, 0, 0.12)">
                            {{ header.text }}
                        </th>
                    </tr>
                </template>
                </thead>
            </template>
            <template 
                v-if="crud.nested"
                v-slot:body="{items}">
                <template v-for="v in crud.headers">
                    <td v-if="!v.children"
                        :key="v.value"
                        :class="`text-xs-${v.align}`">
                        {{ v.format ? v.format(items[v.value]) : items[v.value] }}
                    </td>
                    <td v-else
                        v-for="c in v.children"
                        :key="c.value"
                        :class="`text-xs-${c.align}`">
                        {{ v.format ? v.format(items[v.value]) : items[v.value] }}
                    </td>
                </template>
            </template>
			<template v-slot:[`item.status`]="{item}">
				<v-switch v-model="item.status" readonly class="mt-0" style="height:-webkit-fill-available"/>
			</template>
			<template v-slot:[`item.aksi`]="{item}">
				<v-btn small icon v-on:click="handleOpenFormEdit">
					<v-icon small>
						mdi-pencil
					</v-icon>
				</v-btn>
				<v-btn small icon v-on:click="handleKonfirmasiHapus(item)">
					<v-icon small>
						mdi-delete
					</v-icon>
				</v-btn>
			</template>
		</v-data-table>
        <!-- untuk popup form dan edit -->
        <v-dialog
            v-model="dialogForm"
            max-width="500px"
        >
            <v-card>
                <!-- untuk judul dipopup -->
                <v-card-title>
                    <span class="headline">{{ dialogTitle }}</span>
                </v-card-title>

                <v-card-text>
                    <v-container>
                        <v-form ref="form" v-model="valid">
                            <div 
                                v-for="(item, index) in crud.headers.filter((item)=>item.form!=false)"
                                :key="index">
                                <!-- jika tipenya switct -->
                                <v-switch 
                                    v-if="item.type==='switch'"
                                    :label="item.text"
                                    v-model="item.status" 
                                    class="mt-0" />
                                <!-- jika tipenya number -->
                                <v-text-field
                                    v-else-if="item.type==='number'"
                                    type="number"
                                    :label="item.text"
                                    :messages="item.info"
                                    placeholder="tes"/>
                                <!-- jika tipenya text -->
                                <v-text-field
                                    v-else
                                    :label="item.text"
                                    :messages="item.info"
                                    placeholder="tes"/>
                            </div>
                        </v-form>
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
                    
                >
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
    props: ["crud", "color"],
	data: () => ({
        valid:false,
		dipilih: [],
		dialogForm: false,
		dialogDelete: false,
		dialogTitle: '',
		data: [],
    }),
	methods:{
		handleKonfirmasiHapus(){
			// console.log(this)
			this.dialogDelete	= true
		},
		handleHapus(){
			this.dialogDelete	= false
		},
        handleOpenFormTambah(){
            this.dialogTitle    = "Tambah"
            this.dialogForm     = true
        },
        handleOpenFormEdit(){
            this.dialogTitle    = "Edit"
            this.dialogForm     = true
        },
        processTableHeaders(headers) {
            
            const nested = !!headers.some(h => h.children)
            if (nested) {
                let children = []

                const h = headers.map(h => {
                    if (h.children && h.children.length > 0) {
                        children.push(...h.children)

                        return {
                            rowspan: 1,
                            colspan: h.children.length,
                            text: h.text,
                            align: h.align
                        }
                    }
                    return {
                        rowspan: 2,
                        colspan: 1,
                        text: h.text,
                        align: h.align
                    }
                })

                return {
                    children: children,
                    parents: h
                }
            }
            return {
                parents: headers
            }
        }
	}
}
</script>
