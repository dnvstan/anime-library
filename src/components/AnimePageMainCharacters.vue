<template>
	<section class="characters" v-show="charactersArray.length">
		<AnimePageMainSectionTitle
			:routerPath="{
				name: 'AnimePageCharacters',
				params: currentAnime.mal_id,
			}"
			:viewMoreButton="charactersArray.length > 6"
			>Characters</AnimePageMainSectionTitle
		>
		<transition-group
			class="characters__list"
			tag="ul"
			name="characters-list"
			appear
		>
			<li
				class="characters__item"
				v-for="char in slicedCharactersArray"
				:key="char.character.mal_id"
			>
				<router-link
					class="character__link"
					:to="{
						name: 'CharacterInfoPage',
						params: { charId: char.character.mal_id },
					}"
				>
					<img
						class="character__image"
						:src="char.character.images.jpg.image_url"
						:alt="char.character.name ?? 'Character image'"
					/>
				</router-link>
				<div class="character__info">
					<router-link
						class="character__name"
						:to="{
							name: 'CharacterInfoPage',
							params: { charId: char.character.mal_id },
						}"
					>
						{{ char.character.name }}
					</router-link>
					<div class="character__role">{{ char.role }}</div>
				</div>
			</li>
		</transition-group>
	</section>
</template>

<script>
import AnimePageMainSectionTitle from '@/components/AnimePageMainSectionTitle.vue'
import { mapState } from 'vuex'

export default {
	components: {
		AnimePageMainSectionTitle,
	},

	computed: {
		...mapState({
			currentAnime: (state) => state.animePage.currentAnime,
			charactersArray: (state) => state.animePage.charactersArray,
		}),

		slicedCharactersArray() {
			return this.charactersArray.slice(0, 6)
		},
	},
}
</script>

<style lang="sass" scoped>
.characters
	margin-bottom: 50px

	@media (max-width: $screen-xs-max)
		margin-bottom: 25px

	&__title
		display: flex
		justify-content: space-between

	&__list
		padding: 0
		margin-top: 10px
		margin-bottom: 0
		display: grid
		justify-items: center
		grid-template-columns: 1fr 1fr
		grid-gap: 10px
		list-style: none

		@media (max-width: $screen-xs-max)
			grid-template-columns: 1fr

.characters__item
	width: 100%
	padding: 5px
	display: flex
	border: 1px solid #a8a8a8
	border-radius: 5px

	@media (max-width: $screen-m-max)
		max-width: 400px

.character__info
	display: inline-block

.character__link
	width: 100%
	max-width: 60px
	margin-right: 10px
	display: block

.character__image
	width: 100%
	display: block
	border-radius: 5px

.character__name
	margin-bottom: 5px
	font-weight: 700
	color: #000
	text-decoration: none

	&:hover
		text-decoration: underline
		color: $main-color

.characters-list-enter-from
	opacity: 0
	transform: scale(0.6)

.characters-list-enter-to
	opacity: 1
	transform: scale(1)

.characters-list-enter-active
	transition: all .4s ease
</style>