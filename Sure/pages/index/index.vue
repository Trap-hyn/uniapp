<template>
	<view>
		<image class="in-img" src="https://shp.qpic.cn/ishow/2735031418/1647254062_1265602313_28811_sProdImgNo_7.jpg/0" mode="scaleToFill"></image>
		
		<view class="tip-box">
			<text>还没有登录？</text>
			<text @click="goLogin()" class="color-btn">点我</text>
		</view>
		
		<nui-tiltle title1="会员特供" text1="适合你的攻略才叫攻略!"></nui-tiltle>
		<view class="course-box">
			<view v-for="i in resourseList" :key="i.img" class="public-list">
				<image @click="goCourse()" :src="i.img" mode=""></image>
				<text>{{i.courseName}}</text>
			</view>
			
			<nui-tiltle title1="视频制作" text1="自己成为大佬!"></nui-tiltle>
			<view v-for="i in resourseListByType" :key="i.img" class="public-list">
				<image @click="goCourse()" :src="i.img" mode=""></image>
				<text>{{i.courseName}}</text>
			</view>
			
			<nui-tiltle title1="视频管理" text1="历史记录"></nui-tiltle>
			<view v-for="i in resourseListBySuper" :key="i.img" class="public-list">
				<image @click="goCourse()" :src="i.img" mode=""></image>
				<text>{{i.courseName}}</text>
			</view>
			
			<nui-tiltle title1="视频分类" text1="选择观看分类"></nui-tiltle>
			<view v-for="i in resourseListByGift" :key="i.img" class="public-list">
				<image @click="goCourse()" :src="i.img" mode=""></image>
				<text>{{i.courseName}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			resourseList:[],
			resourseListByType:[],
			resourseListBySuper:[],
			resourseListByGift:[],
			baseUrl:""
			}
		},
		onLoad() {
			let _this = this
			uni.getStorage({
				key: 'token',
					success: function (res) {
					_this.token = res.data
					console.log(_this.token)
					},
				})
			uni.request({
				method:'GET',
			    url: 'https://www.fastmock.site/mock/b9332e460ccb26a4a1cd4e6a393f5522/mp-weixin/getContent', 
			    success: (res) => {
					this.resourseList = res.data.date,
					this.resourseListByType = this.resourseList.filter((m) => m.type == 1),
					this.resourseListBySuper = this.resourseList.filter((m) => m.type == 2),
					this.resourseListByGift = this.resourseList.filter((m) => m.type == 3)
			    }
			});
		},
		methods: {
			goCourse(){
				let _this = this
					if (this.token) {
			
					} else {
						uni.showModal({
							title: '提示',
							content: 'VIP资源需要登录查看',
							success: function(res) {
								if (res.confirm) {
									//进入登录页面
									// console.log('用户点击确定');
									_this.goLogin()
								} else if (res.cancel) {
									// console.log('用户点击取消');
								}
							}
						});
					}
			},
			goLogin() {
				uni.navigateTo({
					url: `/pages/login/login`
				});
			}
		}
	}
</script>

<style scoped>
.in-img{
	width: 100%;
	height: 200px;
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
	.course-box{
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-between;
	}
	.tip-box{
		font-size: 25px;
		font-weight: 600;
		text-align: center;
		margin-bottom: 10px;
	}
	.tip-box .color-btn{
		color: #eb7c06;
	}
</style>
