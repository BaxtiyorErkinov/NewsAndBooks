<template>
	<div>	
	  <v-parallax
	    dark
	    :src="getImageUrl('book-back.jpg')"
	    jumbotron
	    top
	    width="100%"
	  >
	    <v-row
	      align="center"
	      justify="center"
	    >
	      <v-col
	        class="text-center"
	        cols="12"
	      >
	        <h1 class="text-h1 font-weight-bold mb-4">
	          BOOKS
	        </h1>
	      </v-col>
	    </v-row>
	  </v-parallax>
	  <v-container class="d-flex justify-center">
	  	<v-form class="d-flex" @submit.prevent="get_result">  		
		  	<div class="d-flex">
		  		<v-text-field 
		  			outlined 
		  			label="Search Book ..."
		  			v-model="form.query"
		  		/>
		  	</div>
		  	<div class="d-flex ml-2">
		  		<v-btn type="submit" height="55"color="teal accent-3"><v-icon color="white">mdi-magnify</v-icon></v-btn>
		  	</div>
	  	</v-form>
	  </v-container>
	  <v-container v-if="result.length > 0">
	  	<v-container class="grey lighten-2">
	  		<v-row>
	  			<v-col cols='12'>
	  				<h2>Results:</h2>
	  			</v-col>
	  			<v-col cols="12">
					<v-row class="justify-center">
						<v-col cols="12" md="5" v-for="result in result" :key="result.id">
							<v-card flat class="grey lighten-3 pa-5">
								<v-img height="200" :src="`http://127.0.0.1:8000${result.cover}`"></v-img>
								<div class="text-center pa-3 mt-5">
									<h2 class="mb-2">{{result.title}}</h2>
								</div>
								<div class="text-right">
									<a :href="`http://127.0.0.1:8000${result.book}`" class="text-decoration-none"><v-btn class="white--text" color="teal accent-3">DOWNLOAD</v-btn></a>
								</div>
							</v-card>
						</v-col>
					</v-row>
	  			</v-col>
	  			<v-col cols="12" class='gret lighten-3 text-right'>
	  				<div>
	  					<v-btn depressed @click="close_result" class="close">Close</v-btn>
	  				</div>
	  			</v-col>
	  		</v-row>
		</v-container>
	  </v-container>
	  <v-container>
	  	<BookCard />
	  </v-container>
	</div>
</template>
<script>
	export default{
		head: {
      		title: 'Educenter - Books'
    	},
		data(){
			return{
				result: [],
				error: false,
				form: {
					query: ''
				}
			}
		},
		methods:{
			async get_result(){
				await this.$axios.post('http://127.0.0.1:8000/api/booksearch/', this.form)
				.then(res => {
					this.result = res.data
					this.form.query = ''
				})
			},
			getImageUrl(img){
				return require(`~/assets/images/${img}`)
			},
			close_result(){
				this.result.splice(0, 1)
			}
		}
	}
</script>

<style>
</style>