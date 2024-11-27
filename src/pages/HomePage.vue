<template>
	<div class="home">
		<div class="container">
			<h2 class="section__title">Winter 2022</h2>
			<Slider v-slot="{ card }" :contentArr="seasonNow" sliderSize="wide">
				<AnimeCard :animeCard="card" />
			</Slider>

			<h2 class="section__title">Top anime</h2>
			<Slider v-slot="{ card }" :contentArr="topAnime" sliderSize="wide">
				<AnimeCard :animeCard="card" />
			</Slider>

			<h2 class="section__title">Top upcoming anime</h2>
			<Slider v-slot="{ card }" :contentArr="seasonUpcoming" sliderSize="wide">
				<AnimeCard :animeCard="card" />
			</Slider>
		</div>
	</div>
</template>

<script>
import Slider from '@/components/Slider.vue'
import AnimeCard from '@/components/AnimeCard.vue'
import { mapState, mapActions } from 'vuex'

export default {
	name: 'HomePage',
	components: {
		Slider,
		AnimeCard,
	},

	created() {
		this.getTopAnime()
		this.getSeasonNow()
		this.getSeasonUpcoming()
	},

	computed: {
		...mapState({
			topAnime: (state) => state.homePage.topAnime,
			seasonNow: (state) => state.homePage.seasonNow,
			seasonUpcoming: (state) => state.homePage.seasonUpcoming,
		}),
	},

	methods: {
		...mapActions({
			getTopAnime: 'homePage/getTopAnime',
			getSeasonNow: 'homePage/getSeasonNow',
			getSeasonUpcoming: 'homePage/getSeasonUpcoming',
		}),
	},
}
</script>

<style lang="sass" scoped>
.home
	padding-top: 40px
	padding-bottom: 40px
	background-color: #e6e6e6

.container
	@include container

.section__title
	@include container
	@include borderBottom
	padding-bottom: 2px
	margin-bottom: 10px
	font-size: 22px
	color: $dark-black-color

	&:not(:first-child)
		margin-top: 30px
</style>