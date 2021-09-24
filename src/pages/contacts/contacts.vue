<template>
 <view class="box">
<block v-for="(item,index) in contacts" :key="index">
    <view class="card">
        <view class="box1">            
                <image class="image"
                    :src="item.qr_image"
                    mode="scaleToFill"
                />
            <view class="characters">
                <text class="name">{{item.name}}</text>
                <text class="common">{{item.position}}</text>
                <text class="common">{{item.company}}</text>
            </view>
        </view>
        <view class="box2">
            <text>{{item.skill}}</text>
        </view>
        <view class="box3">
            <view class="phone">
                <image
                    src="/static/phone.png"
                    mode="scaleToFill"
                />
                <text>{{item.phone}}</text>
            </view>
            <view class="call" @click="onClick(item.phone)">联系我们</view>
        </view>
    </view>
</block>
</view> 
</template>

<script>
export default {
    onLoad(){
        this.$u.get('http://hello-app.test/api/client/linkmen')
        .then((res)=>{
            this.contacts=res
        })
    },
                data(){
                    return{
                        contacts:[]

                        
                    }
                },
                methods:{
                    onClick(phone){
                        wx.makePhoneCall({
                            phoneNumber: phone
                        })
                    }
                }
}
</script>

<style>
.card{
      width: 670rpx;
      height: 360rpx;
      margin-left: 40rpx;
      margin-right: 40rpx;
      margin-block: 40rpx;
      border-radius: 20rpx;
      box-shadow: 0 0 16rpx 0 rgba(0, 0, 0, 0.16);
      position: relative;
}
.box1{
     width: 610.5rpx;
     height: 220rpx;
     position:absolute;
     top:40rpx;
     left:30rpx;
     right:30rpx;
    border-bottom: 1px solid #E4E4E4;
    display: flex;

}
.image{
    width: 200rpx;
    height: 200rpx;
    margin-right: 30rpx;
}
.characters{
   
   display: flex;
   flex-direction: column; 
}
.name{
    color: #000;
    font-size:36rpx;
    margin-block: 15rpx;
}
.common{
    color: #999999;
    font-size:32rpx;
    margin-block: 15rpx;

}
.box2{
    width: 140rpx;
        height: 48rpx;
        background-color: #003afe;
        border-top-right-radius: 20rpx;
        border-bottom-left-radius: 20rpx;
        position: absolute;
        right: 0;
        top: 0;
        display: flex;
        justify-content: center;
        align-items: center;
}
.box2 text{
    color: #FFFFFF;
}
.box3{
    width: 610rpx;
    position:absolute;
     bottom:20rpx;
     left:30rpx;
     right:30rpx;
    display: flex;
    justify-content: space-between;
}
.phone{
    width: 255rpx;
}
.phone image{
    width: 24rpx;
    height: 24rpx;
    margin-right: 13rpx;
}
.phone text{
    color: #999999;
    font-size:28rpx;
}
.call{
    color: #003AFE;
}
</style>