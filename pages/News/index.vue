<template>
	<div>	
	  <v-parallax
	    dark
	    :src="getImageUrl('back3.jpg')"
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
	          NEWS
	        </h1>
	      </v-col>
	    </v-row>
	  </v-parallax>
	  <v-container>
	  	<NewsCard />
	  </v-container>
	</div>
</template>

<script>
	export default{
		head: {
      		title: 'Educenter - News'
    	},
		methods:{
			getImageUrl(img){
				return require(`~/assets/images/${img}`)
			}
		}
	}
</script>