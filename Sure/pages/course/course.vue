<template>
	<view>
		<image class="banner-img" src="../../static/img/t01.jpg" mode="widthFix"></image>
		<view v-for="(i,index) in course" :key="index" class="course-list">
				<text class="course-title">{{i.courseName}}</text>
				<view class="course-content">
					<image class="course-image" :src="i.img" mode="widthFix"></image>
					<view class="course-text">
						<text>{{i.destext}}</text>
						<button @click="goContent(i.url,i.courseName)" class="btn" size="mini" type="default">立即攻略</button>
					</view>
				</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				course:[]
			}
		},
		methods: {
			goContent(url,title){
				//console.log(url)
				uni.navigateTo({
					//url:'/publicView/publicView?url=${url}&title=${title}'
					 url: `/pages/publicView/publicView?url=${url}&title=${title}`
				});
			}
		},
		onLoad() {
			uni.request({
				method:'GET',
			    url: 'https://www.fastmock.site/mock/b9332e460ccb26a4a1cd4e6a393f5522/mp-weixin/getContent', 
			    success: (res) => {
					this.course = res.data.date
			    }
			});
		}
	}
</script>

<style scoped>
.banner-img{
	width: 100%;
	height: 130px;
}
.course-list{
	padding: 10px;
	text-align: center;
}
.course-content{
	display: flex;
	flex-direction: row;
	margin-top: 10px;
}
.course-content .course-image{
	width: 45%;
	height:100px;
	margin-right: 5px;
}
.course-text{
	display: flex;
	flex-direction: column;
	justify-content: space-between;
	flex: 1;
}
.course-text text{
	font-size: 12px;
	text-align: left;
}
.btn{
	color: #FFFF00;
	background-color: rgb(238,159,32);
	border-color: rbg(238,159,32);
}
</style>
