<template>
	<div>
		<Header title="Perusahaan" to="/apps/perusahaan" :menu="menu"/>
		<nuxt-child></nuxt-child>
	</div>
</template>
<script>
export default {
	layout:'apps',
	data: () => ({
		menu: [
            {
                nama: "Akun Perusahaan",
                link: "/apps/perusahaan/akun",
            },
            {
                nama: "Data Perusahaan",
                link: "/apps/perusahaan/data",
            },
        ]
    }),
	methods:{
		
	}
}
</script>
