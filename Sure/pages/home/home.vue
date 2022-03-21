<template>
	<view>
		<!-- 轮播图 -->
			<swiper class="swiper" :indicator-dots="true" :autoplay="true" :interval="2000" :duration="500">
					<swiper-item v-for="(i,index) in list" :key="i">
						<view class="swiper-item uni-bg-red">
							<image :src="i" mode="aspectFit"></image>
									
						</view>
					</swiper-item>
				</swiper>
				
			<nui-tiltle @getTitle="getTitleFun($event)" title1="游戏" title2="直播" text1="直播互动 " text2="攻略教学"></nui-tiltle>
			
			<view class="public-box">
				<view @click="goPublic(i.url,i.text)"  v-for="i in titleList" :key="i.url" class="public-list" >
					<image :src="i.img" mode=""></image>
					<text>{{i.text}}</text>
				</view>
			</view>
			
			<nui-tiltle  title1="娱乐" title2="天地" text1="让生活不在无聊!!!" ></nui-tiltle>
			
			<view class="retresmail-box">
				<view v-for="(i,index) in etReSmail" :key="index" class="retresmail-list">
					<image :src="i.img"></image>
					<view class="retresmail-text-list">
						<text class="retresmail-title-list">{{i.title}}</text>
						<text class="retresmail-list-text">{{i.text}}</text>
					</view>
				</view>
			</view>
			<nui-tiltle  title1="合作" title2="平台" text1="多端合作畅所欲言" ></nui-tiltle>
			
			<view class="buddy-box">
					<image class="buddy-list" v-for="i in buddy" :src="i.img" :key="i.img"></image>				
			</view>
	</view>
	
</template>

<script>
	export default{
		data(){
			return{
				list : [
					'../../static/img/l01.jpg',
					'../../static/img/l02.jpg',
					'../../static/img/l03.jpg',
					'../../static/img/l04.jpg'],
					
				titleList:[],
				etReSmail:[],
				buddy:[]
			}
		},
		onLoad() {
			uni.request({
				method:'GET',
			    url: 'https://www.fastmock.site/mock/b9332e460ccb26a4a1cd4e6a393f5522/mp-weixin/getPublic', 
			    success: (res) => {
					this.titleList = res.data.date
			    }
			});
			uni.request({
				method:'GET',
			    url: 'https://www.fastmock.site/mock/b9332e460ccb26a4a1cd4e6a393f5522/mp-weixin/getReSmail', 
			    success: (res) => {
					this.etReSmail = res.data.date
			    }
			});
			uni.request({
				method:'GET',
			    url: 'https://www.fastmock.site/mock/b9332e460ccb26a4a1cd4e6a393f5522/mp-weixin/getPfImage', 
			    success: (res) => {
					this.buddy = res.data.date
			    }
			});
		},
		methods:{
			getTitleFun(text){
				console.log(text)
			},
			goPublic(url,title){
				//console.log(url)
				uni.navigateTo({
					//url:'/publicView/publicView?url=${url}&title=${title}'
					 url: `/pages/publicView/publicView?url=${url}&title=${title}`
				});
			}
		}
	}
</script>

<style scoped> 
	.swiper-item image{
		width: 100%;
		/* #ifdef MP */
		height: 150px;
		/* #endif */
		/* #ifdef APP-PLUS */
		height: 200px;
		/* #endif */
	}
	.swiper-item{
		width: 100%;
	}
	.public-box,
	.buddy-box{
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		align-items: center;
		justify-content: space-between;
		padding: 10px;
		border-radius: 10px;
	}
	.public-list{
		width: 48%;
		height: 150px;
		margin-bottom: 20px;
		text-align: center;
		
		
	}
	.public-list image{
		width: 100%;
		height: 120px;
		margin-bottom: 1px;
		border-radius: 10px;
		border: 1px solid #007AFF;
	}
	.public-list text{
		font-size: 14px;
		color: #4CD964;
		line-height: 20px;
	}
	.retresmail-box{
		padding: 10px;
	}
	.retresmail-list{
		display: flex;
		flex-direction: row;
		margin-bottom: 15px;
	}
	.retresmail-list image{
		width: 48%;
		height: 150px;
		margin-right: 10px;
		border-radius: 20px;
	}
	.retresmail-text-list{
		flex: 1;
		/* overflow: hidden; */
		display: flex;
		flex-direction: column;
		color: #333;
		text-align: center;
	}
	.retresmail-title-list{
		width: 100%;
		height: 10px;
		font-weight: 600;
		margin: 5px 0;
	}
	.retresmail-list-text{
		width: 100%;
		height:120px;
		padding: 10px;
		font-size: 12px;
		text-align: left;
	}
	.buddy-box .buddy-list{
		width: 20%;
		height: 30px;
	}
</style>
