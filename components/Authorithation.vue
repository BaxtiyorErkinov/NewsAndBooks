<template>
	<div>
	<v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="8">
            <v-card class="elevation-12">
              <v-window v-model="step" class="pa-2">
                <v-window-item :value="1">
                  <v-row>
                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <h1
                          class="text-center display-2 teal--text text--accent-3"
                        >Sign in</h1>
                        <h4 class="text-center mt-4">Ensure your email for registration</h4>
                        <v-form @submit.prevent="login">
                          <v-text-field
                            label="Email"
                            name="Email"
                            prepend-icon="mdi-email"
                            type="text"
                            color="teal accent-3"
                            v-model="loginForm.username"
                          />

                          <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            prepend-icon="mdi-lock"
                            type="password"
                            color="teal accent-3"
                            v-model="loginForm.password"
                          />
                          <div class="text-center">
                            <v-btn type="submit" rounded color="teal accent-3" dark>SIGN IN</v-btn>
                          </div>
                        </v-form>
                      </v-card-text>
                    </v-col>
                    <v-col cols="12" md="4" class="teal accent-3">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Hello, Friend!</h1>
                        <h5
                          class="text-center"
                        >Enter your personal details and start journay with us</h5>
                      </v-card-text>
                      <div class="text-center">
                        <v-btn rounded outlined dark @click="step++">SIGN UP</v-btn>
                      </div>
                    </v-col>
                  </v-row>
                </v-window-item>
                <v-window-item :value="2">
                  <v-row class="fill-height gray">
                    <v-col cols="12" md="4" class="ma-auto">	           		
                    	<div class="card">    
	                        <h1 class="text-center display-1"><span>Welcome Back!</span></h1>
	                        <h5
	                          class="text-center mt-3"
	                        >To Keep connected with us please login with your personnel info</h5>
	                      <div class="text-center mt-4">
	                        <v-btn rounded outlined color="teal accent-3" @click="step--">Sign in</v-btn>
	                      </div>
                    	</div>
                    </v-col>

                    <v-col cols="12" md="8">
                      <v-card-text class="mt-12">
                        <h1 class="text-center display-2 teal--text text--accent-3">Create Account</h1>
                        <v-form @submit.prevent="submitForm">
                          <v-text-field
                            label="Name"
                            name="Name"
                            prepend-icon="mdi-account"
                            type="text"
                            color="teal accent-3"
                            v-model="form.name"
                          />                          
                          <v-text-field
                            label="Surname"
                            name="surname"
                            prepend-icon="mdi-account"
                            type="text"
                            color="teal accent-3"
                            v-model="form.surname"
                          />
                          <v-text-field
                            label="Username"
                            name="username"
                            prepend-icon="mdi-account"
                            type="text"
                            color="teal accent-3"
                            v-model="form.userlogin"
                          />
                          <v-text-field
                            label="Email"
                            name="Email"
                            prepend-icon="mdi-email"
                            type="text"
                            color="teal accent-3"
                            v-model="form.email"
                          />

                          <v-text-field
                            id="password"
                            label="Password"
                            name="password"
                            prepend-icon="mdi-lock"
                            type="password"
                            color="teal accent-3"
                            v-model="form.password"
                          />
                          <v-text-field
                            label="Country"
                            name="country"
                            prepend-icon="mdi-city"
                            type="text"
                            color="teal accent-3"
                            v-model="form.country"
                          />
                          <v-text-field
                            label="Region"
                            name="region"
                            prepend-icon="mdi-home-city-outline"
                            type="text"
                            color="teal accent-3"
                            v-model="form.region"
                          />
                          <v-select
                          :items="educenters"
                          item-text="title"
                          label="Language"
                          outlined
                          v-model="form.center"
                        ></v-select>
	                      <div class="text-center">
	                        <v-btn type="submit" rounded color="teal accent-3" dark>SIGN UP</v-btn>
	                      </div>
                        </v-form>
                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-window-item>
              </v-window>
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
				step: 1,
        educenters: [],
				form: {
					name: '',
					surname: '',
					userlogin: '',
					password: '',
					email: '',
					country: '',
					region: '',
          center: '',
          user_key: 1
				},
        loginForm: {
          username: '',
          password: ''
        }
			}
		},
		methods: {
			async submitForm(){      
  				await this.$axios.post('https://actions.uz/api/student-create/', this.form) 
            .catch(err => {
              console.log(err)
              this.$nuxt.$emit('auth', false)
            })
          await this.$axios.post('https://actions.uz/api/token/', {
                username: this.form.userlogin,
                password: this.form.password
              }).then(res => {        
                this.$router.push('/v/profile')      
                this.$auth.$storage.setLocalStorage("token", res.data.access)
                this.$auth.$storage.setLocalStorage("refreshToken", res.data.refresh)
              })

			},
      async login(){
          await this.$axios.post('https://actions.uz/api/token/', this.loginForm)
            .then(res => {
              this.$auth.$storage.setLocalStorage("token", res.data.access)
              this.$auth.$storage.setLocalStorage("refreshToken", res.data.refresh)
              this.$router.push('/v/profile')
              console.log(this.$auth.storage.getLocalStorage('token'))
            }).catch(err => {
              this.$nuxt.$emit('auth', false)
            })
      },
      async getEducenters(){        
        this.$axios.get('https://actions.uz/api/educenter-view/')
          .then(res => {
            this.educenters = res.data
          })
      }
		},
    created(){
      this.getEducenters()
    }
	}
</script>

<style scoped>
	span{
		font-family: Ubuntu;
	}
</style>