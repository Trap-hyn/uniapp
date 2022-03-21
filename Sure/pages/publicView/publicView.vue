<template>
	<view>
		<web-view :src="url"></web-view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				url:'https://nz.qq.com/',
				
			}
		},
		onLoad(option) {
			//console.log(option)
			this.url = option.url
			uni.setNavigationBarTitle({
				title:option.title
			})
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
