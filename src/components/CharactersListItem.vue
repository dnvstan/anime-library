<template>
	<li class="character" v-show="char">
		<router-link
			class="character__link"
			:to="{
				name: 'CharacterInfoPage',
				params: { charId: char.character.mal_id },
			}"
		>
			<img
				class="character-image"
				:src="char.character.images.jpg.image_url"
				:alt="char.character.name || 'Character image'"
			/>
		</router-link>
		<div class="character__info">
			<router-link
				class="character__link character__name"
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
</template>

<script>
export default {
	props: ['char'],
}
</script>

<style lang="sass" scoped>
.character
	width: 100%
	height: 110px
	padding-top: 5px
	padding-bottom: 5px
	padding-left: 5px
	display: flex

	&:not(:last-child)
		border-bottom: 2px solid #a3a3a3

	&__link
		width: 100%
		max-width: 60px
		margin-right: 10px

	&-image
		width: 100%
		height: 100%
		display: block
		object-fit: cover
		object-position: center

	&__name
		margin-bottom: 10px
		text-decoration: none
		color: #000
		font-weight: 700

		&:hover
			color: $main-color
			text-decoration: underline

	&:nth-child(even)
		background-color: #ebebeb
</style>