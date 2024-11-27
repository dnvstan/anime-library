<template>
	<footer class="footer">
		<div class="footer__wrapper">
			<div class="footer__content">
				<router-link class="footer__logo" :to="{ name: 'HomePage' }"
					>AniBase</router-link
				>
				<ul class="footer__links-list">
					<li class="footer__item">
						<router-link class="footer__link" :to="{ name: 'HomePage' }">
							Terms of Service
						</router-link>
					</li>
					<li class="footer__item">
						<router-link class="footer__link" :to="{ name: 'HomePage' }">
							Copyright Policy
						</router-link>
					</li>
					<li class="footer__item">
						<router-link class="footer__link" :to="{ name: 'HomePage' }">
							Privacy Policy
						</router-link>
					</li>
					<li class="footer__item">
						<router-link class="footer__link" :to="{ name: 'HomePage' }">
							About
						</router-link>
					</li>
					<li class="footer__item">
						<router-link class="footer__link" :to="{ name: 'HomePage' }">
							Help/FAQ
						</router-link>
					</li>
				</ul>
			</div>
			<div class="footer__copyright">
				AnimeBase is a property of AnimeBase Co.,Ltd. ©2022 All Rights Reserved.
			</div>
			<div class="footer__recaptcha">
				This site is protected by reCAPTCHA and the Google Privacy Policy and
				Terms of Service apply.
			</div>
		</div>
	</footer>
</template>

<script>
export default {}
</script>

<style lang="sass" scoped>
.footer
	width: 100%
	padding-top: 30px
	padding-bottom: 30px
	background-color: $main-color

	&__wrapper
		@include container
		display: flex
		flex-direction: column

	&__content
		margin-bottom: 20px
		display: flex
		align-items: center

	&__logo
		margin-right: 5px
		display: block
		font-family: 'Fredoka-SemiBold'
		font-size: 24px
		line-height: .9
		text-decoration: none
		color: $dark-black-color

	&__links-list
		width: 100%
		padding-left: 0
		margin-top: 0
		margin-bottom: 0
		display: flex
		justify-content: space-evenly
		align-items: center
		list-style-type: none

		@media (max-width: $screen-xs-max)
			flex-direction: column

	&__item
		min-width: 80px
		padding: 8px 10px
		transition: .2s
		text-align: center

		&:hover
			text-decoration: underline

	&__link
		display: block
		color: #000
		text-decoration-line: none

		@media (max-width: $screen-s-max)
			font-size: 14px

	&__copyright
		margin-bottom: 5px
		font-family: 'Fredoka-Light'
		font-size: 15px
		text-align: center

		@media (max-width: $screen-s-max)
			font-size: 13px

	&__recaptcha
		font-family: 'Fredoka-Light'
		font-size: 13px
		text-align: center
</style>