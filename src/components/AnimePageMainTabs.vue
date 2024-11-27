<template>
	<ul class="tabs">
		<li
			v-for="tab in tabs"
			:key="tab.pathName"
			class="tabs__item"
			:class="{ selected: this.$route.name === tab.pathName }"
		>
			<router-link class="tabs__link" :to="{ name: tab.pathName }">
				{{ tab.label }}
			</router-link>
		</li>
	</ul>
</template>

<script>
export default {
	data() {
		return {
			tabs: [
				{ label: 'Details', pathName: 'AnimePageMain' },
				{ label: 'Characters', pathName: 'AnimePageCharacters' },
				{ label: 'Reviews', pathName: 'AnimePageReviews' },
			],
		}
	},
}
</script>

<style lang="sass" scoped>
.tabs
	width: 100%
	padding-left: 0
	margin-top: 0
	margin-bottom: 10px
	display: flex
	justify-content: center
	list-style: none

	&__item
		width: 100%
		max-width: 120px
		background-color: $main-color
		border-radius: 5px

		&:not(:last-child)
			margin-right: 10px

	&__link
		width: 100%
		padding-left: 10px
		padding-right: 10px
		padding-top: 8px
		padding-bottom: 8px
		display: block
		text-decoration: none
		text-align: center
		color: #000

	.selected
		z-index: 5
		background-color: #fffb96
		box-shadow: 0 0 0 2px $light-black-color
		font-family: 'Fredoka-SemiBold', sans-serif

		.tabs__link
			color: $light-black-color
</style>