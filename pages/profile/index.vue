<template>
	<v-app>
		<v-row align="center" justify="center">
			<v-col cols="12" md="4" sm="4">
				<v-card class="grey lighten-3 pa-5 text-center">
					<v-avatar>
						<v-img :src="require('@/assets/images/user.png')"></v-img>
					</v-avatar>
				</v-card>
			</v-col>
		</v-row>
	</v-app>
</template>

<script>
	export default{
		data(){
			return{

			}
		},
		// methods: {		
		// 	async get_user(){
		// 		this.$axios.get('http://127.0.0.1:8000/api/get-user/', this.$auth.$storage.getLocalStorage("token"))
		// 			.then(res => {
		// 				console.log(res)
		// 			})
		// 	}
		// },
		mounted(){
			try{
				this.$axios.get('http://127.0.0.1:8000/api/get-user/', {
					headers: {
	         		 Authorization:"Bearer " + this.$auth.$storage.getLocalStorage("token")
	        	}
				})
				this.$nuxt.$emit('auth', true)
			} catch{
				this.$router.push('/auth')
				this.$nuxt.$emit('auth', false)
			}
		},
		// created(){
		// 	 this.get_user()
		// }
	}
</script>