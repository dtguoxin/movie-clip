<template>
  <div id="app">
    <div class="fill">
      <vue-movie-clip ref="my_movieclip" :auto-play="false" :init-frame="1" width="375px"
                      height="360px" type="canvas" v-show="true" :frame-time="100"
                      :frame="frame" :frames="frames"
                      :loop="false" :forward="forward"
                      @frame="onFrame" @play="onPlay" @stop="onStop" v-if="step<=1">




      </vue-movie-clip>
      <div class="btn" @click="switchState()" v-if="step===0">{{state}}</div>
    </div>



    <!--<div class="btn" @click="switchLoop()">loop:{{loop}}</div>-->
    <!--<div class="btn" @click="switchForward()">forward:{{forward}}</div>-->

  </div>
</template>

<script>

  import fastclick from 'fastclick'
  import VueMovieClip from 'vue-movie-clip'
  import VueFullscreenVideo from "vue-fullscreen-video";
  import imgS1 from "./assets/img/video/00001.jpg"
  import imgS2 from "./assets/img/video/00002.jpg"
  import imgS3 from "./assets/img/video/00003.jpg"
  import imgS4 from "./assets/img/video/00004.jpg"
  import imgS5 from "./assets/img/video/00005.jpg"
  import imgS6 from "./assets/img/video/00006.jpg"
  import imgS7 from "./assets/img/video/00007.jpg"
  import imgS8 from "./assets/img/video/00008.jpg"
  import imgS9 from "./assets/img/video/00009.jpg"
  import imgS10 from "./assets/img/video/00010.jpg"
  import imgS11 from "./assets/img/video/00011.jpg"
  import imgS12 from "./assets/img/video/00012.jpg"
  import imgS13 from "./assets/img/video/00013.jpg"
  import imgS14 from "./assets/img/video/00014.jpg"
  import imgS15 from "./assets/img/video/00015.jpg"
  import imgS16 from "./assets/img/video/00016.jpg"
  import imgS17 from "./assets/img/video/00017.jpg"
  import imgS18 from "./assets/img/video/00018.jpg"
  import imgS19 from "./assets/img/video/00019.jpg"
  import imgS20 from "./assets/img/video/00020.jpg"
  import imgS21 from "./assets/img/video/00021.jpg"
  import imgS22 from "./assets/img/video/00022.jpg"
  import imgS23 from "./assets/img/video/00023.jpg"
  import imgS24 from "./assets/img/video/00024.jpg"
  import imgS25 from "./assets/img/video/00025.jpg"



  function PrefixInteger(num, n) {
    return (Array(n).join(0) + num).slice(-n);
  }
  let frames = [];
  for (let i = 1; i < 26; i++) {
    frames.push('./img/video/' + PrefixInteger(i, 5) + '.jpg')
  }


export default {
    components:{VueMovieClip,VueFullscreenVideo},
  name: 'app',
  data () {
    return {

        frame:25,frames:frames,
        loop:false,forward:true,
        state:"stop",step:0,
    }
  },
  methods:{
    sliderCallback: function (value) {
      this.$refs.my_movieclip.skipTo(value);
    },
    /*switchLoop: function () {
      this.loop = !this.loop
    }, switchForward: function () {
      this.forward = !this.forward
    },*/
    switchState: function () {
      if (this.$refs.my_movieclip.playing) {
        this.$refs.my_movieclip.stop();
      } else {
        this.$refs.my_movieclip.play();
      }
      this.step=1;
    },
    updateState: function () {
      this.state = this.$refs.my_movieclip.playing ? 'stop' : 'play'
    },
    setFrameTime: function (frameTime) {
      this.$refs.my_movieclip.setFrameTime(frameTime);
      this.frameTime = this.$refs.my_movieclip.frameTime;
      console.log(this.frameTime)
    },
    skipTo: function (frame) {
      this.$refs.my_movieclip.skipTo(frame);
    },
    onFrame: function (mc) {
      this.frame = mc.frame;
      // this.width=640-this.frame;
      // console.log(mc.frame)
    },
    onPlay: function (mc) {
      console.log('play')
      this.updateState()
    },
    onStop: function (mc) {
      console.log('stop')
      this.updateState()
      this.step=0;
      //  this.$refs.my_movieclip.skipTo(1);
    }
  },
  mounted: function () {
    fastclick.attach(this.$el)
  },

}
</script>

<style>
@import "assets/css/base.css";
@import "assets/css/mobile_h5.css";
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;width:100%;
}
.pa{
  position: absolute;
  bottom:0px;
  left: 0px;
  width: 100%;
  height: 140px;
  color: #fff;
}
.fill{
  position: relative;width:100%;
}
.btn{
  width: 80px;height:36px;
  line-height: 36px;text-align: center;position: absolute;
  left:0;right:0;top:0;bottom:0;
  margin: auto;
  border: 1px solid #f0f0f0;background: #ccc;
}
</style>
