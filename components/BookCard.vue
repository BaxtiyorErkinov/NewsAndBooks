<template>
	<div>
		<v-container>
			<v-row>
				<v-col cols="12" md="4" v-for="book in allBooks" :key="book.id">
					<v-card flat class="grey lighten-3 pa-5">
						<v-img height="200" :src="`https://actions.uz${book.cover}`"></v-img>
						<div class="text-center pa-3 mt-5">
							<h2 class="mb-2">{{book.title}}</h2>
						</div>
						<div class="text-right">
							<a :href="`https://actions.uz${book.book}`" class="text-decoration-none"><v-btn class="white--text" color="teal accent-3">DOWNLOAD</v-btn></a>
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
				allBooks: []
			}
		},
		methods:{
			async get_books(){
				await this.$axios.get('https://actions.uz/api/book-view/')
					.then(res => {
						this.allBooks = res.data
					})
			}
		},
		created(){
			this.get_books()
		}
	}
</script>