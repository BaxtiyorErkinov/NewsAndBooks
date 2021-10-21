<template>
	<v-container class="my-10">
		<v-row>
			<v-col cols="12" md="7">
				<v-card>
					<v-img :src="`https://actions.uz${news.image}`" height='400'></v-img>
						<div class="text-center">
							<v-btn icon fab><v-icon>mdi-instagram</v-icon></v-btn>
							<v-btn icon fab><v-icon>mdi-facebook</v-icon></v-btn>
							<v-btn icon fab><v-icon>mdi-send-outline</v-icon></v-btn>
						</div>
						<div class="text-center pa-3">
							<h2>{{news.title}}</h2>

							<p>{{news.text}}</p>
						</div>
				</v-card>
			</v-col>
			<v-col cols="12" md="5">			
				<v-card tile flat color="grey lighten-3" class="pa-3">
					<v-card-title>Lates Posts</v-card-title>
					<v-row v-for="today in filteredNews" :key="today.id" v-if="today.id <= 3">				
						<v-col>
							<v-container>							
								<div class="pa-3">
									<v-row>
										<v-col cols="4">
											<v-img :src="`https://actions.uz${today.image}`" height="70"></v-img>
										</v-col>
										<v-col cols="6">
											<h3>{{today.title}}</h3>
											<p>{{today.text}}...</p>
										</v-col>
										<v-col cols="2">
											<a :href="`news/${today.id}`" class="text-decoration-none"><v-btn fab icon text color="orange">
												<v-icon>mdi-arrow-right-bold-circle-outline</v-icon>
											</v-btn></a>
										</v-col>
									</v-row>
								</div>
							</v-container>
						</v-col>
					</v-row>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
	export default{
		data(){
			return{
				news: [],
				allNews: []
			}
		},
		computed:{
			filteredNews(){
				let desc = this.allNews
				desc.map(el => {
					return el.text = el.text.slice(0, 20)
				})
				return desc
			},
		},
		async asyncData({$axios, params}){
			const news = await $axios.$get(`https://actions.uz/api/site-view-single/${params.id}/`)

			return{
				news: news
			}
		},
		mounted(){
			this.$axios.get('https://actions.uz/api/site-view/')
				.then(res => {
					this.allNews = res.data
				})
		}
	}
</script>