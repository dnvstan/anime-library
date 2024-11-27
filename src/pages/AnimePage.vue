<template>
	<div class="container">
		<AnimePageSidebar />
		<div class="main">
			<AnimeTitle />
			<AnimePageMainTabs />
			<router-view />
		</div>
		<ButtonToTop />
	</div>
</template>

<script>
import AnimePageSidebar from '@/components/AnimePageSidebar.vue'
import AnimeTitle from '@/components/AnimeTitle.vue'
import AnimePageMainTabs from '@/components/AnimePageMainTabs.vue'
import ButtonToTop from '@/components/ButtonToTop.vue'
import { mapMutations, mapActions } from 'vuex'

export default {
	components: {
		AnimePageSidebar,
		AnimeTitle,
		AnimePageMainTabs,
		ButtonToTop,
	},

	created() {
		this.getAnimeById(this.$route.params.animeId)
	},

	unmounted() {
		this.SET_CURRENT_ANIME({})
		this.SET_ANIME_INFO({
			animeImage: null,
			animeImageAlt: null,
			categories: [],
		})
		this.SET_TRAILER({})
		this.SET_CHARACTERS_ARRAY([])
		this.SET_REVIEWS_ARRAY([])
		this.SET_RECOMMENDATIONS_ARRAY([])
	},

	methods: {
		...mapMutations({
			SET_CURRENT_ANIME: 'animePage/SET_CURRENT_ANIME',
			SET_ANIME_INFO: 'animePage/SET_ANIME_INFO',
			SET_TRAILER: 'animePage/SET_TRAILER',
			SET_CHARACTERS_ARRAY: 'animePage/SET_CHARACTERS_ARRAY',
			SET_REVIEWS_ARRAY: 'animePage/SET_REVIEWS_ARRAY',
			SET_RECOMMENDATIONS_ARRAY: 'animePage/SET_RECOMMENDATIONS_ARRAY',
		}),

		...mapActions({
			getAnimeById: 'animePage/getAnimeById',
			getCharacters: 'animePage/getCharacters',
			getReviews: 'animePage/getReviews',
		}),
	},
}
</script>

<style lang='sass' scoped>
.container
	@include container
	padding-top: 30px
	padding-bottom: 30px
	display: flex
	position: relative

	@media (max-width: $screen-xs-max)
		flex-direction: column
		font-size: 14px

.main
	width: 100%
	max-width: calc(75% - 20px)
	display: flex
	flex-direction: column

	@media (max-width: $screen-xs-max)
		max-width: 100%
</style>