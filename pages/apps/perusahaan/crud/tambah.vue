<template>
	<div>
		<Head 
			title="Tambah" 
			subtitle="Tambah Proses Penerimaan Peserta Didik Baru"
			back/>
		<v-col class="mx-auto" sm="12" md="6">
			<v-card elevation="2">
				<v-card-text>
					<v-form ref="form" v-model="valid">
						<v-text-field
							label="Nama Proses"
							:messages="['Contoh : Penerimaan Siswa Baru Tahun 2021']"
							:rules="rule.name"/>
						<v-text-field
							label="Kode Awalan"
							:messages="['Contoh : 2021']"
							:rules="rule.name"/>
						<v-text-field
							label="Kode Awalan"
							:messages="['Contoh : Penerimaan Siswa Baru Tahun 2017']"
							:rules="rule.name"/>
						<v-text-field
							label="Jumlah Siswa yang diterima"
							:messages="['Contoh : 200']"
							type="number"
							:rules="rule.name"/>
						<div class="text-right">
							<v-btn 
								:disabled="!valid"
								type="submit"
								color="primary">
								Simpan
							</v-btn>
						</div>
					</v-form>
				</v-card-text>
			</v-card>
		</v-col>
	</div>
</template>
<script>
export default {
	data: () => ({
		valid: false,
		rule:{
			name:[
				v => !!v || 'Username harus diisi',
			],
			password:[
				v => !!v || 'Password harus diisi',
			]
		}
    }),
	methods:{
		handleSubmit:()=>{

		}
	}
}
</script>
