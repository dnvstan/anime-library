<template>
	<transition name="title" appear>
		<h1 class="anime-title" v-show="animeTitle">
			{{ animeTitle }}
		</h1>
	</transition>
</template>

<script>
import { mapState } from 'vuex'
export default {
	computed: {
		...mapState({
			currentAnime: (state) => state.animePage.currentAnime,
		}),

		animeTitle() {
			return this.currentAnime.title_english
				? this.currentAnime.title_english
				: this.currentAnime.title
		},
	},
}
</script>

<style lang="sass" scoped>
.anime-title
	margin-top: 0
	margin-bottom: 20px
	font-size: 26px
	font-weight: 800

	@media (max-width: $screen-xs-max)
		margin-bottom: 10px
		display: none
		font-size: 18px

.title-enter-from
	opacity: 0
	transform: translateY(-15px)

.title-enter-to
	opacity: 1
	transform: translateX(0)

.title-enter-active
	transition: all .4s ease
</style>