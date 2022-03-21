<template>
	<view>
		<view @click="getText" class="title-box">
			<text>{{title1}}</text>
			<text class="title2">{{title2}}</text>
		</view>
		<view class="text-box">
			<text>{{text1}}</text>
			<text>{{text2}}</text>
		</view>
	</view>
</template>

<script>
	export default {
		name:"nui-tiltle",
		props:{
			title1:String,
			title2:String,
			text1:String,
			text2:String
		},
		data() {
			return {
				
			};
		},
		methods:{
			getText(){
				this.$emit('getTitle',this.title1+this.title2)
			}
		}
	}
</script>

<style scoped>
	.uni-tiltle-box{
		margin: 10px auto;
	}
	.title-box,
	.text-box{
		text-align: center;
	}
	.title-box{
		font-size: 20px;
		font-weight: 600;
		text-shadow: 2px 2px 2px rgb(98 98 98 / 52%);
	}
	.text-box{
		color: #999;
		line-height: 30px;
	}
	.title2{
		color: #ffff00;
	}
</style>
