<template>
  <div class="container">
    <div class="mp-list">
      <navigator class="item"
        target="miniProgram"
        open-type="navigate"
        :app-id="item.appId"
        version="release"
        v-for="(item, index) in miniPrograms" 
        :key="index"
      >
        <div class="left">
          <img :src="item.icon">
        </div>
        <div class="right">
          
          <div class="name">{{item.name}}</div>
          <div class="desc">{{item.desc}}</div>
        </div>
      </navigator>
    </div>
    <div class="contact">
      <contact-button 
        type="default-light"
        session-from="weapp">联系客服
      </contact-button>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      miniPrograms: [
        {
          name: '语音合成tts',
          icon: '../../static/miniProgramsIcons/tts.png',
          appId: 'wx29a19992eacac173',
          path: 'page/index/main',
          desc: '语音在线合成、文本转语音。对接多平台(讯飞、思必驰、百度)，多发音人可选，可调语速、并可提供下载链接。'
        },
        {
          name: '水印plus',
          icon: '../../static/miniProgramsIcons/sy.png',
          appId: 'wx2a01aefc88bbe77a',
          path: 'page/index/main',
          desc: '给图片（主要是用于证件）加上指定文字的水印，服务端不会存储用户的任何图片信息，可直接断网使用。'
        },
        {
          name: '每月缴税计算',
          icon: '../../static/miniProgramsIcons/gs.png',
          appId: 'wx2d58df3cd62ac8b0',
          path: 'page/index/main',
          desc: '2019最新个税计算，生成每月应缴税列表'
        },
        {
          name: 'MyRegister',
          icon: '../../static/miniProgramsIcons/myregister.png',
          appId: 'wxcb7e75e7a6a8d5c6',
          path: 'page/index/index',
          desc: '管理保存注册的手机号码或者邮箱应用或网站，由于现在大部分人拥有多个手机或邮箱，解决注册信息主要是手机或邮箱记忆紊乱的问题'
        }
      ]
    }
  },
  mounted () {
    wx.setNavigationBarTitle({
      title: '其它小程序'
    })
    wx.setNavigationBarColor({
      frontColor: '#000000',
      backgroundColor: '#3D4C65',
      animation: {
        duration: 400,
        timingFunc: 'easeIn'
      }
    })
    wx.setBackgroundColor({
      backgroundColor: '#3D4C65' // 窗口的背景色为白色
    })
  }
}
</script>

<style scoped>
.container{
  background-color: #3D4C65;
  padding-bottom: 200rpx;
}
.item {
  width: 720rpx;
  margin: 15rpx 0 30rpx 0;
  padding: 0 0 15rpx 0;
  display: flex;
  background-color: rgb(255, 255, 255);
  border-radius: 10rpx;
}
.item .left{
  width: 180rpx;
  padding: 15rpx;
}
.item .left img{
  margin-top: 15rpx;
  width: 150rpx;
  height: 150rpx;
  border: 1rpx solid rgb(202, 202, 202);
}
.item .right{
  width: 530rpx;
  padding-left: 20rpx;
  color: #4D5F80;
  font-size: 36rpx;
}
.item .right .name {
  margin-top: 15rpx;
  height: 48rpx;
  line-height: 48rpx
}
.item .right .desc {
  text-indent: 56rpx;
  margin-top: 10rpx;
  font-size: 28rpx;
  line-height: 32rpx;
}

.contact{
  width: 720rpx;
  height: 150rpx;
  padding: 15rpx;
  font-size: 24rpx;
  text-align: center;
  color: #cccccc;
}
</style>
