<template>
	<div class="pos">
		<v-row class="pos">			
			<v-col cols="4">
				<v-card height="15" flat tile class="mt-10 opacity" color="#2da397"></v-card>
			</v-col>
			<v-col cols="4">
				<v-card height="15" flat tile class="mt-10 opacity" color="#f16101"></v-card>		
			</v-col>
			<v-col cols="4">
				<v-card height="15" flat tile class="mt-10 opacity" color="#7c4bc0"></v-card>
			</v-col>
		</v-row>
	</div>
</template>

<style scoped>
	.pos{
		/*position: absolute;*/
		width: 100%;
		top: 1.5%;
		/*z-index: 2000;*/
		/*background: transparent;*/
	}
	.opacity{
		opacity: 0.9;
	}
</style>