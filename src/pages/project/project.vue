<template>
    <view class="box">
        <!-- <u-navbar back-text=" " title="百景" is-fixed="true"></u-navbar> -->
        <view class="page">
        <view class="content"> 
        <view class="uni-padding-wrap uni-common-mt">
            <video class="myVideo" :src="project.uil" show-mute-btn="ture" :poster="project.img" ></video>
        </view>
        <view class="about">
            <view>
            <text class="name">项目名称：{{project.name}}</text>
            <block v-for="i in project.hot" :key="i">
				<image class="hot" src="/static/fire.png"></image>
			</block>
            </view>
            <view class="date">
                <text>上传时间：{{project.creationTime}}</text>
            </view>
            <text class="middleSized">项目合作方：{{project.company}}</text>
            <text class="middleSized">项目投入资金：{{project.money}}</text>
            <text class="middleSized">项目周期：{{project.cycle}}</text>
        </view>
        <view class="particulars">
            <u-parse :html="project.Introduction"></u-parse>
        </view>
        </view>
        <view class="footer" @click="toPage">联系我们</view>
        </view>

    </view>
</template>

<script>

    export default {
    onLoad: function (option){
            this.id = option.id
 			this.$u.get('http://hello-app.test/api/client/project/' + this.id )
				.then((res)=>{
					this.project = res
				
				})                 
    },    
                data(){
                    
                    return{
                        id:'',
                        project:{
                        }
                    }
                },
                methods:{
                    toPage(){
                        uni.switchTab({ url: '/pages/contacts/contacts' })
                    }
                }
        
    }
</script>

<style lang="scss" scoped>
.box{
  height: 100%;
  width: 100vw;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
   padding: 0;
   margin: 0;
  
}
.page{
    box-sizing: border-box;
    width: 100vw;
    height: 100vh;
    display: flex;
  flex-direction: column;

}
.myVideo{
    margin-top: 0%;
    width: 100%;
    margin-block: 40rpx;

}
.about{

    width: 689rpx;
    margin-left :30rpx;
	margin-right: 30rpx;
    border-bottom: 1px solid #E4E4E4;
    display: flex;
    flex-direction: column;
}
.name{
    font-size: 46rpx;
    margin-right: 20rpx;
}
.hot{
	width: 24rpx;
	height: 31rpx;
    margin-right: 10rpx;
}
.date{
    font-size: 24rpx;
    color: #999999;
    margin-block: 40rpx;
}
.middleSized{
    font-size: 32rpx;
    margin-block: 30rpx;
    color: #000;
}
.particulars{
    margin-left :30rpx;
	margin-right: 30rpx;
}
  .footer {
  height: 95rpx;
  margin-top: 22rpx;
  padding: 8px 0;
  background-image: linear-gradient(to right, #003afe, #4a00e0);
  color: #fff;
  font-size: 36rpx;
  display: flex;
  justify-content: center;
  align-items: center;
     padding: 0;
   margin: 0;
}
.content{
    box-sizing: border-box;
  flex: 1;
  overflow-y: auto;
}
</style>