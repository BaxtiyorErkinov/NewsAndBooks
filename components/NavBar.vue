<template>
	<nav>
		<v-app-bar fixed flat elevate-on-scroll>
			<v-toolbar-title class="black--text ml-3 mr-4">Kepso</v-toolbar-title>
			    <v-spacer></v-spacer>
			        <v-toolbar-items class="align-center hidden-sm-and-down"> 
			        	<div>
							<v-btn icon>
								<v-hover color="orange" v-slot="{ hover }">
									<v-icon size="23" tag="i" :color="hover ? 'orange' : 'gray'">mdi-twitter</v-icon>
								</v-hover>

							</v-btn>
							<v-btn icon>
								<v-hover color="orange" v-slot="{ hover }">
									<v-icon size="23" :color="hover ? 'orange' : 'gray'">mdi-facebook</v-icon>
								</v-hover>
							</v-btn>
							<v-btn icon>
								<v-hover color="orange" v-slot="{ hover }">
									<v-icon size="23" :color="hover ? 'orange' : 'gray'">mdi-instagram</v-icon>
								</v-hover>
							</v-btn>
							<v-btn icon>
								<v-hover color="orange" v-slot="{ hover }">
									<v-icon size="23" :color="hover ? 'orange' : 'gray'">mdi-send-outline</v-icon>
								</v-hover>
							</v-btn>
						</div>			         
       			        <ul v-for="item in nav" :key="item.id">
					        <li>
					  			<nuxt-link exact :to="`/${item.link}`" class="hovered">{{item.title}}</nuxt-link>        		
					        </li>
					    </ul>
				    </v-toolbar-items>
				    <v-spacer />
		      	<div class="d-flex">
					    <v-list-item v-if="auth" @click="logout" class="hidden-sm-and-down" link><span class="auth grey--text font-weight-bold"><v-icon>mdi-logout</v-icon>Logout</span></v-list-item>
					    <v-list-item v-else class="hidden-sm-and-down" link to="/auth"><span class="auth grey--text font-weight-bold">Login / Register</span></v-list-item>
			    </div>
				    <v-app-bar-nav-icon 
				    	@click="drawer = !drawer"
				        color="grey" 
				        class="hidden-md-and-up">
			        </v-app-bar-nav-icon>
		</v-app-bar>
		      	<v-navigation-drawer app v-model="drawer" color="white" width="150" right class="hidden-md-and-up">
				        <v-list v-for="item in nav" :key="item.id">
				         	<v-list-item link :to="item.link">
				         		<span class="grey--text font-weight-bold">{{item.title}}</span>
				         	</v-list-item>

				        </v-list>
				        <v-list class="text-start">
				        	 <v-list-item v-if="auth" @click="logout"><span class="auth grey--text font-weight-bold"><v-icon>mdi-logout</v-icon>Logout</span></v-list-item>
					    	<v-list-item v-else link to="/auth"><span class="auth font-weight-bold grey--text">Login / Register</span></v-list-item>
				        </v-list>
		      	</v-navigation-drawer>
	    </nav>
</template>

<script>
	export default{
		data(){
			return{
				drawer: false,			
				nav:[
					{
						id: 1,
						title: 'Home',
						link: '' 
					},
					{
						id: 2,
						title: 'Pages',
						link: 'pages' 
					},
					{
						id: 3,
						title: 'Courses',
						link: 'courses' 
					},
					{
						id: 4,
						title: 'Teachers',
						link: 'teachers'
					},
					{
						id: 5,
						title: 'News',
						link: 'news' 
					},
					{
						id: 6,
						title: 'Contact',
						link: 'contact' 
					},
					{
						id: 7,
						title: 'Profile',
						link: 'profile'
					},
					{
						id: 8,
						title: 'Books',
						link: 'books'
					}
				],
				auth: false
			}
		},
		methods:{
			async logout(){
				await this.$axios.post('https://actions.uz/api/token/refresh/', {
					refresh: this.$auth.$storage.getLocalStorage('refreshToken')
				})
				.then(res => {
	        	this.$router.push('/v/auth')
						this.$auth.$storage.removeLocalStorage('refreshToken')
						this.$auth.$storage.removeLocalStorage('token')

	        })
			}
		},
	mounted(){
      this.$nuxt.$on('auth', auth => {
        this.auth = auth
      })
    }
	}
</script>

<style scoped>
 .full{
 	width: 100px;
 }
 .nuxt-link-active{
 	color: orange;
 }
 .hovered:hover{
 	color: orange;
 }
 li a{
 	text-decoration: none;
 }
 li a{
 	color: grey;
 	font-weight: bold;
 	font-family: Ubuntu;
 }
 li{
 	list-style: none;
 	font-size: 16px;
 }
 .hovered{
 	transition: all .5s;

 }
 i:hover{
 	font-style: orange;
 }
 .auth{
 	color: #81868a;
 }
 .links{
 	margin: 0 auto;
 }
</style>