<template>
	<v-container class="fill-height pb-3 pb-sm-5">
		
		<!-- preview card -->
		<v-card 
			:elevation="$vuetify.breakpoint.xsOnly ? 8 : 24" 
			:width="$vuetify.breakpoint.xsOnly ? 320 : 600" 
			class="mx-auto"
		>			
			<v-row align="center" class="mx-0" :class="linkParams.color">
				<v-col class="my-4 my-sm-10">
					<v-sheet 
						:width="roundSize"
						:height="roundSize"
						color="white" 
						class="mx-auto pt-1 round shadow"
					>
						<v-sheet 
							:width="roundSize - 8"
							:height="roundSize - 8"
							class="d-flex ml-1 round secondary"
						>

							<!-- preview card icon -->
							<v-icon class="mx-auto no-transition" :class="linkParams.textColor" size="108">
								{{ linkParams.icon }}
							</v-icon>
						</v-sheet>
					</v-sheet>
				</v-col>
			</v-row>

			<!-- preview card description -->
			<v-card-text class="body-1 accent--text pb-0 pb-sm-4">
				<p 
					class="mb-0" 
					:class="{
						'body-2': $vuetify.breakpoint.xsOnly, 
						'body-1': $vuetify.breakpoint.smAndUp
					}"
				>
					Предлагаем вам пройти тест на знание английских слов.
				</p>
				<p 
					class="mb-0" 
					:class="{
						'body-2': $vuetify.breakpoint.xsOnly, 
						'body-1': $vuetify.breakpoint.smAndUp
					}"
				>
					Тест состоит из 20 вопросов на тему <strong>«{{ linkParams.text }}»</strong>.
				</p>
				<p class="mb-0 d-none d-sm-block">
					В режиме <strong>«слово-перевод»</strong> вам будет предложено выбрать 
					правильный перевод английского слова на русский.<br>
				</p>
				<p class="mb-0 d-none d-sm-block">
					В режиме <strong>«перевод-слово»</strong> нужно будет выбрать правильный 
					английский перевод для русского слова.
				</p>
			</v-card-text>

			<!-- preview card buttons -->
			<v-card-actions class="pt-2 pt-sm-1">
				<v-row class="px-3">
					<v-col class="pb-1 py-sm-3">
						<v-btn 
							class="white--text px-4"
							:class="linkParams.color"
							depressed
							rounded
							block
						>Слово — Перевод</v-btn>
					</v-col>
					<v-col class="py-2 py-sm-3">
						<v-btn 
							class="white--text px-4"
							:class="linkParams.color"
							depressed
							rounded
							block
						>Перевод — Слово</v-btn>
					</v-col>
				</v-row>
			</v-card-actions>
		</v-card>

	</v-container>
</template>

<script>
export default {
	props: {
		links: {
			type: Array,
			required: true
		},
		name: {
			type: String,
			required: true
		}
	},
	computed: {
		// find and return params for current route
		linkParams() {
			const params = {};

			this.links.forEach(item => {
				if (item.route.indexOf(this.name) !== -1) {
					params.icon = item.icon;
					params.text = item.text;
					params.color = item.color;
					params.textColor = item.textColor;
				}
			})

			return params;
		},
		// return size for preview round v-sheet
		roundSize() {
			let size;

			switch (this.$vuetify.breakpoint.name) {
				case 'xs':
					size = '128'
					break
				case 'sm': case 'md': case 'lg': case 'xl':
					size = '198'
					break
			}

			return size
		}
	}
}
</script>

<style>
.round {
	border-radius: 50%;
}
.shadow {
  box-shadow: 0px 25px 35px 0px rgba(0, 0, 0, 0.2);
}
.no-transition {
	transition: none !important;
}
</style>