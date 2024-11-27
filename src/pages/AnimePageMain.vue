<template>
	<AnimePageMainAbout />
	<AnimePageMainCharacters />
	<AnimePageMainReviews />
	<AnimePageMainRecommendations />
</template>

<script>
import AnimePageMainAbout from '@/components/AnimePageMainAbout.vue'
import AnimePageMainCharacters from '@/components/AnimePageMainCharacters.vue'
import AnimePageMainReviews from '@/components/AnimePageMainReviews.vue'
import AnimePageMainRecommendations from '@/components/AnimePageMainRecommendations.vue'

export default {
	components: {
		AnimePageMainAbout,
		AnimePageMainCharacters,
		AnimePageMainReviews,
		AnimePageMainRecommendations,
	},
}
</script>