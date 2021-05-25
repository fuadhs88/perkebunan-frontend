<template>
	<v-col class="mx-auto" sm="12" md="6">
		<v-card elevation="2">
			<v-img
				height="300"
				src="http://localhost:3000/bg.jpg"
				>
				
				<v-img class="mx-8 my-8" width="80" src="https://upload.wikimedia.org/wikipedia/commons/3/37/Coat_of_Arms_of_Regency_Kutai_Timur.png"/>
				
			</v-img>
			<v-card-title>Selamat datang di SIBUNGKIL</v-card-title>
			<v-card-subtitle>
				Sistem Informasi Perkebunan dengan teknologi unggulan terbaik.
			</v-card-subtitle>

			<v-card-text>
				<div>
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
							to="apps"
							type="submit"
							color="primary">
							Masuk
						</v-btn>
					</div>
				</v-form>
				</div>
				
			</v-card-text>
		</v-card>
	</v-col>
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
