<template>
	<transition name="button-to-top" appear>
		<button
			class="button-scroll-to-top"
			v-show="isButtonActive"
			@click="backToTop"
		>
			↑
		</button>
	</transition>
</template>
<script>
export default {
	data() {
		return {
			isButtonActive: false,
		}
	},

	created() {
		window.addEventListener('scroll', () => {
			const offsetY = window.pageYOffset
			this.getPageHeight / 3 > offsetY
				? (this.isButtonActive = false)
				: (this.isButtonActive = true)
		})
	},

	computed: {
		getPageHeight() {
			return Math.max(
				document.body.scrollHeight,
				document.documentElement.scrollHeight,
				document.body.offsetHeight,
				document.documentElement.offsetHeight,
				document.body.clientHeight,
				document.documentElement.clientHeight
			)
		},
	},

	methods: {
		backToTop() {
			window.scroll({ top: 0, behavior: 'smooth' })
		},
	},
}
</script>
<style lang="sass">
.button-scroll-to-top
	@include button
	width: 50px
	height: 50px
	margin-top: auto
	position: fixed
	bottom: 20%
	left: 10%
	font-size: 22px
	z-index: 10

	@media(max-width: $screen-s-max)
		display: none

.button-to-top-enter-from,
.button-to-top-leave-to
	opacity: 0
	transform: translateX(10px)

.button-to-top-enter-to,
.button-to-top-leave-from
	opacity: 1
	transform: translateX(0)

.button-to-top-enter-active,
.button-to-top-leave-active
	transition: all .4s ease
</style>