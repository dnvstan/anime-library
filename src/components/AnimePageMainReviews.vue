<template>
	<section class="reviews" v-show="reviewsArray.length">
		<AnimePageMainSectionTitle
			:routerPath="{
				name: 'AnimePageReviews',
				params: { animeId: currentAnime.mal_id },
			}"
			:viewMoreButton="reviewsArray.length > 4"
		>
			Reviews
		</AnimePageMainSectionTitle>
		<transition-group class="reviews__list" tag="ul" name="reviews-list" appear>
			<li
				class="reviews__item"
				v-for="review in slicedReviewsArray"
				:key="review.mal_id"
			>
				<img
					:src="review.user.images.jpg.image_url"
					alt="User image"
					class="reviews__user-image"
				/>
				<div class="reviews__info">
					<div class="reviews__date">
						{{ review.date }}
					</div>
					<div class="reviews__username">{{ review.user.username }}</div>
					<p class="reviews__text">
						{{ review.review.substring(0, 250) }}...
					</p>
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
			reviewsArray: (state) => state.animePage.reviewsArray,
		}),

		slicedReviewsArray() {
			return this.reviewsArray.slice(0, 5)
		},
	},
}
</script>

<style lang="sass" scoped>
.reviews
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
		list-style: none

	&__item
		padding: 10px
		display: flex
		align-items: flex-start
		border: 1px solid #a8a8a8
		border-radius: 5px
		overflow-x: hidden

		&:not(:last-child)
			margin-bottom: 10px

	&__user-image
		max-width: 60px
		margin-right: 10px
		display: block
		border-radius: 5px

	&__username
		margin-bottom: 5px
		font-weight: 700

	&__text
		margin-top: 0
		margin-bottom: 0

	&__date
		margin-bottom: 5px
		font-size: 14px

.reviews-list-enter-from
	opacity: 0
	transform: translateX(150px)
	
.reviews-list-enter-to
	opacity: 1
	transform: translateX(0)

.reviews-list-enter-active
	transition: all .4s ease
</style>