<template>
	<v-row>
		<v-col md="4" cols="12" class="mx-auto my-auto">
			<div class="align-center" style="margin-top:7rem;">
				<v-card v-if="perusahaan">
					<v-card-title>
						Pilih perusahaan
					</v-card-title>
					<v-divider/>
					<v-card-text>
						<v-radio-group v-model="perusahaanDipilih" dense>
							<v-radio
								v-for="(item, index) in perusahaan"
								:key="index"
								:label="item.nama"
								:value="item.id"
							></v-radio>
						</v-radio-group>
					</v-card-text>
					<v-card-actions>
						<div class="text-right" style="width:100%">
							<v-btn 
								class="primary"
								v-on:click="handelPilihPerusahaan">
								Lanjutkan
							</v-btn>
						</div>
					</v-card-actions>
				</v-card>
				<div v-else>
					<v-img
						src="https://prod-notion-assets.s3-us-west-2.amazonaws.com/front/product/hero.png"/>
					<h2 class="mb-3 mt-3">Mohon tunggu . . .</h2>				
				</div>
			</div>
			<v-divider/>
		</v-col>
		<v-dialog
			v-model="isFetching"
			hide-overlay
			persistent
			width="300"
			>
			<v-card
				color="primary"
				dark
			>
				<v-card-text>
				Memproses ...
				<v-progress-linear
					indeterminate
					color="white"
					class="mb-0"
				></v-progress-linear>
				</v-card-text>
			</v-card>
		</v-dialog>
	</v-row>
</template>
<script>
export default {
	layout:'blank',
	async asyncData({ $axios, $auth }) {
		let info			= false
		const queryString 	= window.location.href;
		const urlParams 	= new URLSearchParams(queryString)
		const token 		= `Bearer ${urlParams.get('access_token')}`
		const tipe			= $auth.$storage.getUniversal("loginType")
		let perusahaan		= false
		let perusahaanDipilih = 1
		await $axios.$post(`v1/akun/masukGoogle`,{
			token:token,
			tipe:tipe,
			device:2,
			token_device:'',
		}).then((resp)=>{
			if(resp.status){	
				$auth.$storage.setUniversal("authToken", resp.data)
				$auth.$storage.setUniversal("_token.google", token)
				if(tipe==="admin"){
					window.location.href='/apps/beranda'
				}else{
					if(resp.perusahaan.length===0){
						window.location.href='/apps/beranda'
					}else{
						perusahaan			= resp.perusahaan
						perusahaanDipilih	= perusahaan[0].id
					}
					
				}
			}else{
				if(confirm(resp.message)){
					window.location.href='/'
				}
			}
		})
		return {
			info,
			perusahaan,
			perusahaanDipilih,
			isFetching: false
		}
	},
	methods:{
		handelPilihPerusahaan: async function(){
			this.isFetching	= true
			const api 		= this.$axios.create({
				headers: {"Authorization": localStorage.getItem("auth.authToken")}
			})
			// Set baseURL to something different
			// api.setBaseURL(process.env.API_URL)
			await api.$get(`v1/akun/perusahaan/${this.perusahaanDipilih}`).then(async (resp)=>{
				await this.$auth.$storage.setUniversal("authToken", resp.data)
				window.location.href='/apps/beranda'
			})
		}
	}
	
}
</script>
<style>
body{
	font-size: 1.5em; /* currently ems cause chrome bug misinterpreting rems on body element */
}
</style>
