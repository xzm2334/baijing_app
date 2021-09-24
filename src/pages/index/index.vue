<template>
	<view class="box">
			<u-tabs :list="list" :current="current" :is-scroll="true" @change="onTabChange" bg-color="#EEEEEE" height="88"></u-tabs>	
		<view class = "content">
		<view class="lunbo" >
			<u-swiper height="260" :list="banner" name="image_url" img-mode=“aspectFit” indicator-pos="bottomRight"></u-swiper>
		</view>
		<!-- <u-gap height="40" /> -->

		<block  v-for="(item,index) in project" :key="index">
		<view class="project" @click="goProject(item.id)">
			<image style="width: 670rpx; height: 360rpx;border-radius: 20rpx;" :src="item.image_uil"></image>
			<view class="title">
			<text class="projectName">项目名称: {{item.name}}</text>
			<block v-for="i in item.hot" :key="i">
				<image class="hot" src="/static/fire.png"></image>
			</block>
			<text class="data">{{item.data}}</text>
			</view>
			</view>
		</block>	
		</view>
	</view>
	
</template>

<script>

	export default {


		data() {
			return {
				id: '',
				project:[
					
				],
				banner:[
					
				],
				list: [],
				current: 0
			}
		},
		onLoad() {
			this.$u.get('http://hello-app.test/api/client/categories')
			.then((res)=>{
					this.list = res
					this.id = this.list[0].id
					this.$u.get('http://hello-app.test/api/client/categories/banners/' + this.id )
					.then((res)=>{
					this.banner = res
				})
					this.$u.get('http://hello-app.test/api/client/categories/projects/' + this.id )
					.then((res)=>{
					this.project = res
					console.log(res);
				})
				})
		},
		methods: {
			onTabChange(index){
				this.current = index
				this.id = this.list[index].id
				this.$u.get('http://hello-app.test/api/client/categories/banners/' + this.id )
				.then((res)=>{
					this.banner = res
				})
				this.$u.get('http://hello-app.test/api/client/categories/projects/' + this.id )
				.then((res)=>{
					this.project = res
				})

			},

			goProject(id){
				this.$u.route('/pages/project/project',{id :id})
			}
		}
	}
</script>

<style>

.content{
	margin-left :40rpx;
	margin-right: 40rpx;
}
.lunbo{
	width:670rpx;
	height: 260rpx;
	margin-block: 60rpx;
	
}
.project{
	margin-block: 60rpx;
}
.title{
	width: 650rpx;
    margin-top: 20rpx;
    display: flex;
    align-items: center;
}
.projectName{
	font-size: 28rpx;
	color: #333333;
	margin-right: 18rpx;
}
.hot{
	width: 24rpx;
	height: 31rpx;
	margin-right: 10rpx;
}
.data{
	flex: 1;
	text-align: right;
	font-size: 28rpx;
	color: #333333;
}
</style>
