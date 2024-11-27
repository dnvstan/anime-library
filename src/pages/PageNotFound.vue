<template>
	<div class="container">
		<h1 class="error-title">Ooops... Page not found. 😢</h1>
	</div>
</template>
<script>
export default {}
</script>
<style lang="sass" scoped>
.container
	@include container
	position: relative

.error-title
	margin-top: 0
	margin-bottom: 0
	position: absolute
	top: 30%
	left: 50%
	text-align: center
	transform: translate(-50%, 50%)

	@media(max-width: $screen-xs-max)
		font-size: 26px
</style>