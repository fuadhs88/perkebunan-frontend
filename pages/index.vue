<template>
	<div class="d-flex" style="height:100vh;">
	<v-col class="mx-auto my-auto" xs="12" md="8" style="justify-content:center">
		<v-card elevation="4">
			<v-row no-gutters>
			<v-col xs="12" md="5" class="primary d-flex" cols="12">
				<div class="mx-auto my-auto text-center">
					<v-icon color="white" size="64">mdi-palm-tree</v-icon>
					<p class="display-1 white--text">SIBUNGKIL</p>
				</div>
			</v-col>
			<v-col xs="12" md="7">
				<v-card-title>Masuk</v-card-title>
				<v-card-subtitle>Sistem Informasi Perkebunan dengan teknologi terbaik</v-card-subtitle>
				<v-card-text>
					<v-form ref="form" v-model="valid" v-on:submit.prevent="handleSubmit">
						<v-text-field
							prepend-icon="mdi-account-circle"
							label="Username"
							:rules="rule.name"/>
						<v-text-field
							prepend-icon="mdi-eye"
							label="Password"
							type="password"
							:rules="rule.password"/>
						<div class="text-right">
							<!-- <v-btn 
								:disabled="!valid"
								type="submit"
								color="primary">
								Masuk
							</v-btn> -->
							<v-btn 
								to="/apps2/beranda"
								color="primary">
								Masuk
							</v-btn>
						</div>
					</v-form>
				</v-card-text>
			</v-col>
			</v-row>
		</v-card>
	</v-col>
	</div>
</template>
<script>
export default {
	layout:'blank',
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
			alert("wkwk")
			return false;
		}
	}
}
</script>
