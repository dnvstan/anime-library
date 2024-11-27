<template>
	<div class="character">
		<div class="container" v-show="Object.keys(currentChar).length">
			<transition class="character__image" name="character-image" appear>
				<img
					v-if="currentChar.images"
					:src="currentChar.images.jpg.image_url"
					:alt="currentChar.name ?? 'Character image'"
				/>
			</transition>
			<div class="character__wrapper">
				<transition name="character-name" appear>
					<h2 class="character__name" v-if="currentChar.name">
						{{ currentChar.name }}
					</h2>
				</transition>
				<transition name="character-description" appear>
					<p
						v-if="currentChar.hasOwnProperty('about')"
						class="character__description"
						:class="{
							'no-info': !currentChar.about,
						}"
					>
						{{ currentChar.about ?? `Sorry we don't have any information` }}
					</p>
				</transition>
			</div>
		</div>
		<h2 class="character__error" v-if="errorCatcher">
			Ooops... Something went wrong. Try reloading. 😢
		</h2>
	</div>
</template>

<script>
import axios from 'axios'

export default {
	data() {
		return {
			currentChar: {},
			errorCatcher: false,
		}
	},

	created() {
		this.getCurrentChar(this.$route.params.charId)
	},

	unmounted() {
		this.currentChar = {}
	},

	methods: {
		async getCurrentChar(id) {
			try {
				const res = await axios.get(`https://api.jikan.moe/v4/characters/${id}`)
				this.currentChar = res.data.data
				this.errorCatcher = false
			} catch (err) {
				console.error(err)
				const errStatus = err.response.data.status
				if (errStatus >= 400 && errStatus <= 500) {
					this.errorCatcher = true
				}
			}
		},
	},
}
</script>

<style lang="sass" scoped>
.character
	padding-top: 30px
	padding-bottom: 30px
	position: relative

	.container
		@include container
		display: flex
		align-items: flex-start

		@media(max-width: $screen-xs-max)
			flex-direction: column

	&__image
		width: 100%
		max-width: 300px
		padding-left: 10px
		padding-right: 10px
		margin-right: 15px
		display: block
		object-fit: contain
		object-position: top

		@media(max-width: $screen-xs-max)
			margin-right: auto
			margin-left: auto
			margin-bottom: 10px

	&__name
		margin-top: 0
		margin-bottom: 10px
		font-size: 24px

	&__description
		margin-top: 0
		margin-bottom: 0
		white-space: pre-line

	&__error
		width: 100%
		padding-left: 10px
		padding-right: 10px
		margin-top: 0
		margin-bottom: 0
		position: absolute
		top: 30%
		left: 50%
		transform: translate(-50%, -50%)
		text-align: center
		font-size: 28px

		@media(max-width: $screen-xs-max)
			font-size: 22px

.no-info
	font-style: italic

.character-image-enter-active,
.character-name-enter-active,
.character-description-enter-active
	transition: all .4s ease

.character-image-enter-from
	opacity: 0
	transform: scaleX(0.6)

.character-image-enter-to
	opacity: 1
	transform: scaleX(1)

.character-name-enter-to
	opacity: 1
	transform: translateX(0)

.character-name-enter-from
	opacity: 0
	transform: translateY(-20px)

.character-description-enter-from
	opacity: 0
	transform: translateX(50px)

.character-description-enter-to
	opacity: 1
	transform: translateX(0)
</style>