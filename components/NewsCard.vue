<template>
	<div>
		<v-container>
			<v-row>
				<v-col cols="12" md="4" v-for="news in filteredNews" :key="news.id">
					<v-card flat class="grey lighten-3 pb-10" width="300">
						<v-img width="300" :src="`https://actions.uz${news.image}`"></v-img>
						<div class="text-center mt-3">
							<v-btn icon fab><v-icon>mdi-instagram</v-icon></v-btn>
							<v-btn icon fab><v-icon>mdi-facebook</v-icon></v-btn>
							<v-btn icon fab><v-icon>mdi-send-outline</v-icon></v-btn>
						</div>
						<div class="text-center pa-3 mt-5">
							<h2 class="mb-2">{{news.title}}</h2>

							<p>{{news.text}}  ...</p>
						</div>
						<div class='text-center'>
							<a :href="`news/${news.id}`" class="readMore">READ MORE</a>
						</div>
					</v-card>
				</v-col>
			</v-row>
		</v-container>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				allNews:[]
			}
		},
		computed:{
			filteredNews(){
				let desc = this.allNews
				desc.map(el => {
					return el.text = el.text.slice(0, 40)
				})
				return desc
			}
		},
		methods:{
			async getNews(){
				await this.$axios.get('https://actions.uz/api/site-view/')
					.then(res => {
						this.allNews = res.data
					})
			}
		},
		mounted(){
			console.log(this.filteredNews)
		},
		created(){
			this.getNews()
		}
	}
</script>

<style scoped>
	.readMore{
		text-decoration: none;
		font-family: sans-serif;
		font-weight: bold;
		color: #000;
		transition: all .5s;
		letter-spacing: 10;
	}
	.readMore:hover{
		color: orange;
	}
</style>