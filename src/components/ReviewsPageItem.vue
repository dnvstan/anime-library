<template>
	<li class="reviews__item">
		<img
			class="reviews__item__image"
			:src="review.user.images.jpg.image_url"
			alt="User image"
		/>
		<div class="reviews__item__wrapper">
			<div class="reviews__item__username">
				{{ review.user.username }}
			</div>
			<div class="reviews__item__review">
				{{ isReadMoreClicked ? review.review : getShortText(review.review) }}
			</div>
			<button class="reviews-button" @click="handleReadMoreButton()">
				{{ buttonContent }}
			</button>
		</div>
	</li>
</template>

<script>
export default {
	props: ['review'],
	data() {
		return {
			isReadMoreClicked: false,
			reviewText: '',
			buttonContent: 'Read more',
		}
	},

	methods: {
		getShortText(text) {
			return text.substring(0, 350) + '...'
		},

		handleReadMoreButton() {
			this.isReadMoreClicked = !this.isReadMoreClicked
			this.isReadMoreClicked
				? (this.buttonContent = 'Read less')
				: (this.buttonContent = 'Read more')
		},
	},
}
</script>
<style lang="sass" scoped>
.reviews__item
	padding-top: 15px
	padding-bottom: 15px
	padding-left: 10px
	padding-right: 10px
	display: flex
	align-items: flex-start

	&:not(:last-child)
		border-bottom: 2px solid #a3a3a3

	&:nth-child(even)
		background-color: #ebebeb

	&__image
		width: 100%
		max-width: 60px
		margin-right: 10px
		object-fit: contain
		object-position: top

	&__username
		margin-bottom: 10px
		font-weight: 700

	&__review
		margin-bottom: 10px

.reviews-button
	@include button
</style>