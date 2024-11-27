<template>
	<div class="title__wrapper">
		<h2 class="section-title">
			<slot></slot>
		</h2>
		<router-link
			class="button-view-more"
			v-if="routerPath && viewMoreButton"
			:to="routerPath"
			@click="clickHandler"
		>
			View more
		</router-link>
	</div>
</template>

<script>
export default {
	props: ['routerPath', 'viewMoreButton'],
	methods: {
		clickHandler() {
			window.scroll({ top: 0, behavior: 'smooth' })
		},
	},
}
</script>

<style lang="sass" scoped>
.title__wrapper
	@include borderBottom
	width: 100%
	padding-bottom: 2px
	display: flex
	align-items: center
	justify-content: space-between

.section-title
	margin: 0
	font-weight: 700
	font-size: 20px

.button-view-more
	@include button
	display: block
	text-decoration: none
	font-size: 12px
</style>