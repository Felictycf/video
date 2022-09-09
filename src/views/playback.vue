<template>
  <div class="playbackView">
    <h3>网路电视</h3>
    <p>Current Type: <span class="badge badge-success">mp4</span></p>
    <video-player class="vjs-custom-skin" ref="videoPlayer" :options="playerOptions">
    </video-player>

    <div class="optionsWrapper">
      <div class="form-group row">
        <label for="" class="col-sm-4 col-form-label">Playback: </label>
        <div class="col-sm-8">
          <input class="form-control" type="text" placeholder="playback url here" v-model="url">
        </div>
        <div class="w-100 mt-3 text-center">
          <button class="btn btn-primary" @click="handleApply">加载链接里面的内容</button>
        </div>
        <div class="w-100 mt-3 text-center">
<!--          添加频道，添加响应式 ，并添加click 事件-->
          <button class="btn btn-primary" @click="handleApply1">电视频道一</button>
          <button class="btn btn-primary" @click="handleApply2">电视频道二</button>
          <button class="btn btn-primary" @click="handleApply3">电视频道三</button>
          <button class="btn btn-primary" @click="handleApply4">电视频道四</button>
        </div>
<!--        订阅-->
<div class="pos">
<!-- 事件进行绑定 ，之后将 数据push 进行数组之后，进行保存，之后进入-->
  <button class="btn btn-primary" @click="recode" >收藏此节目</button>
  <button class="btn btn-primary" @click="selectList" >查看收藏的节目</button>
</div>
        <div class="w-100 mt-3 text-center">
<!--          数据的双向绑定，将数据进行双向绑定，通过 v-show 来判断是否显示-->
          <button v-show="vedio.flag !=1" class="btn btn-primary" @click="vedioPlay1">{{vedio.data1}}</button>
          <button v-show="vedio.flag !=1" class="btn btn-primary" @click="vedioPlay2">{{vedio.data2}}</button>
          <button v-show="vedio.flag !=1" class="btn btn-primary" @click="vedioPlay3">{{vedio.data3}}</button>
<!--          <button class="btn btn-primary" @click="handleApply4">电视频道四</button>-->
        </div>
<div>点击你要播放的卫视</div>
      </div>
    </div>
<!--实现视频播放组件-->
    <Switcher></Switcher>
    <div v-show="show.flag !=1" class="pos1">
      <Select id="ee"  v-model="model1" style="width:200px">
        <Option v-for="item in createnamearr" :value="item" :key="item">{{ item }}</Option>
      </Select>

    </div>
  </div>
</template>

<script>
import Switcher from '@/components/Switcher'
export default {
  name: 'playback',
  components: {
    Switcher
  },
  data () {
    return {
      //配置响应式数据进行响应
      createnamearr:[],
      vedio :{
        flag:1
      },
      show :{
        flag: 1
      },
      //填写频道数据，配置视频服务器地址
      vedioSourc1 :{
        data1 :'湖北卫视',
        data2 :'湖南卫视',
        src1 :'http://fegre.cn:8081/download?url=hubei.mp4',
        src2 :'http://fegre.cn:8081/download?url=hunan.mp4',
        src3 :'http://fegre.cn:8081/download?url=anhui.mp4',
        data3 : '安徽卫视',
      },
      vedioSourc2 :{
        data1 :'山东卫视',
        data2 :'浙江卫视',
        data3 : '江西卫视',
        src1 :'http://fegre.cn:8081/download?url=sandong.mp4',
        src2 :'http://fegre.cn:8081/download?url=zejiang.mp4',
        src3 :'http://fegre.cn:8081/download?url=jiangxi.mp4',
      },

      vedioSourc3 :{
        data1 :'广东卫视',
        data2 :'吉林卫视',
        data3 : '陕西卫视',
        src1 :'http://fegre.cn:8081/download?url=guangdong.mp4',
        src2 :'http://fegre.cn:8081/download?url=jiling.mp4',
        src3 :'http://fegre.cn:8081/download?url=sanxi.mp4',
      },
      vedioSourc4 :{
        data1 :'天津卫视',
        data2 :'江苏卫视',
        data3 : '西藏卫视',
        src1 :'http://fegre.cn:8081/download?url=tianjing.mp4',
        src2 :'http://fegre.cn:8081/download?url=jiangshu.mp4',
        src3 :'http://fegre.cn:8081/download?url=xizhang.mp4',
      },
      url: '',
      playerOptions: {
        autoplay: false,
        controls: true,
        sources: [{
          type: "video/mp4",
          src: "https://cdn.theguardian.tv/webM/2015/07/20/150716YesMen_synd_768k_vp8.webm"
        }]
      }
    }
  },
  methods: {
    //将数据进行响应，之后进行数据的调用
    handleApply () {
      this.playerOptions.sources[0].src = this.url
    },
    handleApply1 () {
      // this.playerOptions.sources[0].src = this.url
      this.vedio=this.vedioSourc1
    },
    handleApply2 () {
      this.vedio=this.vedioSourc2
    },
    handleApply3 () {
      this.vedio=this.vedioSourc3
    },
    handleApply4 () {
      this.vedio=this.vedioSourc4
    },
    // 配置所有的数据源
    vedioPlay1(){
      this.playerOptions.sources[0].src=this.vedio.src1
    },
    vedioPlay2(){
      this.playerOptions.sources[0].src=this.vedio.src2
    },
    vedioPlay3(){
      this.playerOptions.sources[0].src=this.vedio.src3
    },
    // 将频道进行收藏
    recode(){
      window.alert("收藏成功")
      this.createnamearr.push(this.vedio.data1)
      this.createnamearr.push(this.vedio.data2)
      this.createnamearr.push(this.vedio.data3)
    },
    selectList(){
this.show.flag=2
    }

  }
}
</script>

<style scoped>
.playbackView {
  position: relative;
}

.optionsWrapper {
  width: 500px;
  margin: 20px auto;
}
.pos{
  display: inline-block;
  position: relative;
  left: 700px;
  bottom: 150px;
}
.pos1{
  position: relative;
  left: 550px;
  bottom: 200px;
}
</style>
