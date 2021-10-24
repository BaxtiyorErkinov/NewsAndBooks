<template>
	<div>		    	
	  <v-parallax
	    dark
	    :src="getImageUrl('back3.jpg')"
	    top
	    class="pa-0 px-0 ll"
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

<style scoped>

</style>