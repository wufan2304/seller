<template>
	<div class="shopcart">
		<div class="content">
			<div class="content-left">
				<div class="logo-wrapper">
					<div class="logo">
						<span class="icon-shopping_cart"></span>
					</div>
				</div>
				<div class="price">
					
				</div>
				<div class="desc">
					
				</div>

			</div>
			<div class="content-right"></div>
		</div>
	</div>
	
</template>

<script type="text/ecmascript-6">
	export default {};
	
</script>

<style lang="stylus" rel="stylesheet/stylus">
.shopcart
	position: fixed
	left: 0
	bottom: 0
	z-index: 50
	width: 100%
	height: 48px
	.content
		display: flex
		background-color: #141d27
		.content-left
			flex: 1
			.logo-wrapper
				display: inline-block
			.price
				display: inline-block
			.desc
		.content-right
			flex: 0 0 105px
			widht: 105px
</style>