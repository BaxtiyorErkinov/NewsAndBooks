<template>
	<div>
		<v-app-bar fixed flat scroll-threshold>
					<div class="navigation align-center">
						<v-row>
							<v-col cols="2" width="100">
								<div class="items black--text ml-3 mr-4"><h1>Kepso</h1></div>
							</v-col>
							<v-col cols="8">
						    <div class="align-center hidden-sm-and-down items"> 
							     <div class="d-flex">
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
			       			  <ul v-for="item in nav" :key="item.id" class="items">
								        <li>
								  			<nuxt-link exact :to="`/${item.link}`" class="hovered">{{item.title}}</nuxt-link>        		
								        </li>
								    </ul>
							    </div>
							</v-col>
							<v-col cols="2">
					      <div class="items buttons pa-2">
					      		<v-btn v-if="auth" text class="grey--text hidden-sm-and-down">Logout<v-icon>mdi-logout</v-icon></v-btn>
					      		<v-btn v-else text class="grey--text hidden-sm-and-down" link to="/auth">Login / Register</v-btn>
						    </div>
							</v-col>							
								
								<div class="pos mt-sm-12 mt-md-14 mt-12 ml-n1">
				      			<Lines/>  	
								</div>
						</v-row>
							    <v-app-bar-nav-icon 
							    	@click="drawer = !drawer"
							        color="grey" 
							        class="hidden-md-and-up float-right"
							        >
						      </v-app-bar-nav-icon> 								
					</div>
		</v-app-bar>
		      	<v-navigation-drawer app v-model="drawer" color="white" width="150" right class="hidden-md-and-up">
				        <v-list v-for="item in nav" :key="item.id">
				         	<v-list-item link :to="`/${item.link}`">
				         		<span class="grey--text font-weight-bold">{{item.title}}</span>
				         	</v-list-item>

				        </v-list>
				        <v-list class="text-start">
				        	 <v-list-item v-if="auth" @click="logout"><span class="auth grey--text font-weight-bold"><v-icon>mdi-logout</v-icon>Logout</span></v-list-item>
					    	<v-list-item v-else link to="/auth"><span class="auth font-weight-bold grey--text">Login / Register</span></v-list-item>
				        </v-list>
		      	</v-navigation-drawer>	
	    </div>
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
	        	this.$router.push('/auth')
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
 .pos{
 	display: flex;
 	position: absolute;
 	width: 100%;
 	top: 4px;
 	/*background-color: red;*/
 }
 .center{	
 	position: absolute;
 	/*top: 33px;*/
 	max-height: 1px;
 }
 .navigation{
 	width: 100%;
 	display: flex;
 	justify-content: space-between;	
 }
 .items{
 	display: flex;
 }
 .buttons{
 	margin-right: 150px;
 	width: 100%;
 }
</style>