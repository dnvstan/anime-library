<template>
	<h2 class="characters__title">Characters</h2>
	<transition-group
		class="characters__list"
		tag="ul"
		name="characters-list"
		appear
	>
		<CharactersListItem
			v-for="char in charactersArray"
			:key="char.character.mal_id"
			:char="char"
		/>
	</transition-group>
</template>

<script>
import CharactersListItem from '@/components/CharactersListItem.vue'
import { mapState, mapActions } from 'vuex'

export default {
	components: {
		CharactersListItem,
	},

	created() {
		if (this.charactersArray.length === 0) {
			this.getCharacters(this.$route.params.animeId)
		}
	},

	computed: {
		...mapState({
			charactersArray: (state) => state.animePage.charactersArray,
		}),
	},

	methods: {
		...mapActions({
			getCharacters: 'animePage/getCharacters',
		}),
	},
}
</script>

<style lang="sass" scoped>
.characters__title
	margin-top: 0
	margin-bottom: 10px

.characters__list
	width: 100%
	padding-left: 0
	margin-top: 0
	margin-bottom: 0
	display: flex
	flex-direction: column
	list-style: none

.characters-list-enter-from
	opacity: 0
	transform: translateX(100px)

.characters-list-enter-to
	opacity: 1
	transform: translateX(0)

.characters-list-enter-active
	transition: all .4s ease
</style>