<template>
  <div id="app">
    <!--<vue-fullscreen-video style="position: absolute" ref="player"-->
                          <!--:auto-play="false" :loop="false"-->
                          <!--align="crop"-->
                          <!--:url="video" :style="{background: '#000',width:'100%',height:'200px'}"-->
                          <!--&gt;-->

    <!--</vue-fullscreen-video>-->
        <vue-movie-clip ref="my_movieclip" :auto-play="true" :init-frame="10" width="375px"
                        height="360px" type="canvas" v-show="true" :frame-time="frameTime"
                        :frame="frame" :frames="frames"
                        :loop="loop" :forward="forward"
                        @frame="onFrame" @play="onPlay" @stop="onStop">

        </vue-movie-clip>


    <div class="btn" @click="switchState()">{{state}}</div>
    <div class="btn" @click="switchLoop()">loop:{{loop}}</div>
    <div class="btn" @click="switchForward()">forward:{{forward}}</div>

  </div>
</template>

<script>

  import fastclick from 'fastclick'
  import VueMovieClip from 'vue-movie-clip'
  import VueFullscreenVideo from "vue-fullscreen-video";
  import video from "./assets/videos/row.mp4";

  function PrefixInteger(num, n) {
    return (Array(n).join(0) + num).slice(-n);
  }
  let frames = [];
  for (let i = 1; i < 220; i++) {
    frames.push('./assets/img/video/' + PrefixInteger(i, 5) + '.jpg')
  }

export default {
    components:{VueMovieClip,VueFullscreenVideo},
  name: 'app',
  data () {
    return {
        frameTime:20,
        frame:5,frames:frames,
        loop:true,forward:true,
        video:video,state:"stop",
    }
  },
  methods:{
    sliderCallback: function (value) {
      this.$refs.my_movieclip.skipTo(value);
    },
    switchLoop: function () {
      this.loop = !this.loop
    }, switchForward: function () {
      this.forward = !this.forward
    },
    switchState: function () {
      if (this.$refs.my_movieclip.playing) {
        this.$refs.my_movieclip.stop();
      } else {
        this.$refs.my_movieclip.play();
      }
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

      //  this.$refs.my_movieclip.skipTo(1);
    }
  },
  mounted: function () {
    fastclick.attach(this.$el)
  }
}
</script>

<style>
@import "assets/css/base.css";
@import "assets/css/mobile_h5.css";
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
.btn {
  padding: 5px 10px 5px 10px;
  background: #2b81af;
  color: #fff;
  float: left;
  margin: 3px;
  cursor: pointer;
  -webkit-user-select: none;
}
.btn:hover {
  padding: 5px 10px 5px 10px;
  background: #ff0000;
}
.pa{
  position: absolute;
  bottom:0px;
  left: 0px;
  width: 100%;
  height: 140px;
  color: #fff;
}

</style>
