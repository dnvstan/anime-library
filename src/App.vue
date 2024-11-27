<template>
	<div class="page__body">
		<page-header />
		<router-view class="page__content" />
		<page-footer />
	</div>
</template>

<script>
import PageHeader from '@/components/PageHeader.vue'
import PageFooter from '@/components/PageFooter.vue'
export default {
	components: {
		PageHeader,
		PageFooter,
	},
}
</script>

<style lang="sass" scoped>
.page__body
	min-height: 100vh
	display: flex
	flex-direction: column
	position: relative

.page__content
	flex-grow: 1
</style>
