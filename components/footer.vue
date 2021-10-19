<template>
	<div class="cont">	
		<v-row>
			<v-col cols="12">
					<div class="main">
						<v-container>					
							<v-row>
								<v-col cols="6" md="4" class="pa-5">
									<v-card flat color="#022c46" class="white--text box mx-5">
										<div>
											<a class="font white--text name">Courses</a>
										</div>
										<div>
											<a class="grey--text font subtitle d-block">Introduction Web Design</a>
											<a class="font white--text teach">Mike Hardson</a>
										</div>
										<div>
											<a class="grey--text font subtitle d-block">Introduction Web Design</a>
											<a class="font white--text teach">Jessica Brown</a>
										</div>
									</v-card>
								</v-col>
								<v-col cols="6" md="4" center class="pa-5">
								<v-card flat color="#022c46" class="white--text mx-5">
										<div>
											<a class="font white--text name">Explore</a>
										</div>
										<div>
											<a class="grey--text font">About</a>
										</div>
										<div>
											<a class="font grey--text">Overview</a>
										</div>
										<div>
											<a class="grey--text font">Teachers</a>
										</div>
										<div>
											<a class="font grey--text">Join Us</a>
										</div>
										<div>
											<a class="font grey--text">Our News</a>
										</div>
										<div class="my-5">
											<a class="font grey--text d-block">Contact</a>
											<a class="font grey--text">Register Now</a>
										</div>
									</v-card>
								</v-col>
								<v-col cols="12" md="4" class="pa-5">
									<div>
										<a class="name white--text hidden-sm-and-down">Gallery</a>
									</div>	
									<div class="text-center">
										<a class="name white--text hidden-md-and-up">Gallery</a>
									</div>
									<v-container>								
										<v-row class="my-2">
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-1.webp" />
											</v-col>
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-2.jpg" />
											</v-col>
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-3.jpg" />
											</v-col>
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-4.jpg" />
											</v-col>
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-5.jpg" />
											</v-col>
											<v-col cols="6" md="4">
												<v-img src="https://actions.uz/static/images/footer-6.jpg" />
											</v-col>
										</v-row>
									</v-container>
								</v-col>
							</v-row>
						</v-container>
					</div>		
			</v-col>
			<v-col cols="12">
					<div class="about">
						<v-row>
							<v-col cols="12">
								<v-container>
									<v-card flat color="#012237" class="text-center">
										<h3 class="grey--text">About</h3>
										<v-card-subtitle class="grey--text">
											Lorem ipsum dolor sit ametcon, sectetur adipiscing elit. Phasellus vehic sagittis euismod.
										</v-card-subtitle>
										<v-card-actions>
											<v-spacer /> 
											<v-btn tile class="white--text font font-weight-bold" color="#f16101">Contact</v-btn>
											<v-btn tile class="white--text font font-weight-bold" color="#2da397">Purchase</v-btn>
											<v-spacer />
										</v-card-actions>
									</v-card>
								</v-container>
							</v-col>
						</v-row>
					</div>	
			</v-col>
			<v-col cols="6">				
			<div class="made text-center">
				<v-container>
					<h4 class="grey--text">© Copyright 2021 by Baxtiyor Erkinov</h4>
				</v-container>
			</div>
			</v-col>
			<v-col cols="6">			
				<div class="links text-center">
					<v-btn icon color="grey"><v-icon>mdi-instagram</v-icon></v-btn>
					<v-btn icon color="grey"><v-icon>mdi-twitter</v-icon></v-btn>
					<v-btn icon color="grey"><v-icon>mdi-facebook</v-icon></v-btn>
					<v-btn icon color="grey"><v-icon>mdi-send-outline</v-icon></v-btn>
				</div>
			</v-col>
		</v-row>		
	</div>
</template>
<style scoped>
	/*#c*/
	/*012237*/
	.cont{
		background: #012237;
	}
	.main{
		background: #022c46;
		margin: 0;
	}
	.about{
		background: #012237;
		margin: 0;

	}
	.made{
		background: #012237;
	}
	.links{
		background: #012237;
	}
/*	.font{
		margin: 10px 0;
		cursor: pointer;
		font-family: sans-serif;
	}*/
	.name{
		font-size: 30px;
	}
	.subtitle{
		font-size: 20px;
	}
	.teach{
		font-size: 18px;
	}
	.box{
		padding: 0 10px;
	}
</style>