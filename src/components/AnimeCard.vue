<template>
	<router-link
		class="card"
		:to="{ name: 'AnimePageMain', params: { animeId: animeCard.mal_id } }"
	>
		<img
			v-show="Object.keys(animeCard).length"
			class="card__image"
			:src="animeCard.images.jpg.image_url"
			:alt="cardTitle ?? 'Anime poster'"
		/>
		<div class="card__info">
			<div class="card__title">
				{{ cardTitle }}
			</div>
			<div class="card__episodes">
				{{ cardEpisodes }}
			</div>
		</div>
	</router-link>
</template>

<script>
export default {
	props: {
		animeCard: Object,
	},
	computed: {
		cardTitle() {
			return this.animeCard.title_english
				? this.animeCard.title_english
				: this.animeCard.title
		},
		cardEpisodes() {
			const ep = this.animeCard.episodes
			return `${ep ? ep : ''} ${ep > 0 ? 'ep.' : 'Soon'}`
		},
	},
}
</script>

<style lang="sass" scoped>
.slider__wrapper
	@include container
	padding-left: 10px
	padding-right: 10px

.card
	width: 100%
	display: flex
	flex-direction: column
	background-color: #fff
	border-radius: 5px
	overflow: hidden
	text-decoration: none
	transition: all .2s ease

	&:hover
		opacity: .85
		box-shadow: -12px 0 20px -12px rgba(0, 0, 0, 0.35), 12px 0 20px -12px rgba(0, 0, 0, 0.35)

	&__image
		height: 200px
		display: block
		object-fit: cover
		object-position: center center

		@media (max-width: $screen-xs-max)
			height: 190px

	&__info
		padding-left: 10px
		padding-right: 10px
		padding-bottom: 10px
		margin-top: 7px

	&__title
		margin-top: 0
		margin-bottom: 5px
		color: $dark-black-color
		font-weight: 700
		white-space: nowrap
		text-overflow: ellipsis
		overflow: hidden

		@media (max-width: $screen-s-max)
			font-size: 13px

	&__episodes
		color: lighten($dark-black-color, 25%)

		@media (max-width: $screen-s-max)
			font-size: 12px
</style>