<template>
	<h2 class="reviews__title">Reviews</h2>
	<transition-group class="reviews__list" name="reviews-list" tag="ul" appear>
		<ReviewsPageItem
			v-for="review in reviewsArray"
			:key="review.mal_id"
			:review="review"
		/>
	</transition-group>
</template>

<script>
import ReviewsPageItem from '@/components/ReviewsPageItem.vue'
import { mapState, mapActions } from 'vuex'

export default {
	components: {
		ReviewsPageItem,
	},

	created() {
		if (this.reviewsArray.length === 0) {
			this.getReviews(this.$route.params.animeId)
		}
	},

	computed: {
		...mapState({
			reviewsArray: (state) => state.animePage.reviewsArray,
		}),
	},

	methods: {
		...mapActions({
			getReviews: 'animePage/getReviews',
		}),
	},
}
</script>

<style lang="sass" scoped>
.reviews__list
	padding-left: 0
	margin-top: 0
	margin-bottom: 0
	list-style: none

.reviews__title
	margin-top: 0
	margin-bottom: 10px

.reviews-list-enter-from
	opacity: 0
	transform: scaleY(0.6)

.reviews-list-enter-to
	opacity: 1
	transform: scaleY(1)

.reviews-list-enter-active
	transition: all .4s ease
</style>