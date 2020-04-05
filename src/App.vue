<template>
  <div class="app">
    <div class="border" ref="border" />
    <VideoBackground
      v-for="(sources, index) in videos"
      :key="`video-${index}`"
      :sources="sources"
    />

    <h1 class="title" ref="title">Pavel Gonzales</h1>
    <div ref="button">
      <Button>Read resume</Button>
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import { TimelineMax, TweenLite, Linear, Power4 } from 'gsap'
import VideoBackground from '@/components/VideoBackground.vue'
import Button from '@/components/Button.vue'

export default {
  mounted () {
    const borderSize = Math.min(window.innerWidth - 30, window.innerHeight - 30) / 2
    const speed = 2 // sec
    this.tlEntry
      .from(this.$refs.border, speed, { borderWidth: borderSize, scale: 1.04, ease: Power4.easeOut }, 0)
      .from(this.$refs.title, 3, { opacity: 0, y: -20, ease: Power4.easeOut }, 1.5)
      .from(this.$refs.button, 3, { opacity: 0, y: 30, ease: Power4.easeOut }, 1.5)

    setTimeout(() => {
      this.tlEntry.play()
    }, 300) 
  },

  data () {
    return {
      tlEntry: new TimelineMax({ paused: true }),
      tlButton: new TimelineMax({ paused: true }),
      videos: [
        // [
        //   {
        //     src: require('./assets/videos/Ideas.webm'),
        //     type: 'video/webm'
        //   },
        //   {
        //     src: require('./assets/videos/Ideas.mp4'),
        //     type: 'video/mp4'
        //   }
        // ],
        // [
        //   {
        //     src: require('./assets/videos/Flamez.webm'),
        //     type: 'video/webm'
        //   },
        //   {
        //     src: require('./assets/videos/Flamez.mp4'),
        //     type: 'video/mp4'
        //   }
        // ],
        // [
        //   {
        //     src: require('./assets/videos/steps.mp4'),
        //     type: 'video/mp4'
        //   }
        // ],
        [
          {
            src: require('./assets/videos/sea.mp4'),
            type: 'video/mp4'
          }
        ]
      ]
    }
  },
  components: {
    VideoBackground,
    Button
  }
}
</script>
<style>
body {
  font-family: 'Open Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
}

.app {
  min-height: 100vh;
  display: flex;
  flex-wrap: wrap;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.border {
  position: absolute;
  top: 15px;
  left: 15px;
  width: calc(100% - 30px);
  height: calc(100% - 30px);
  border: 25px solid #fff;
  z-index: 1;
  box-sizing: border-box;
  pointer-events: none;
}

.title {
  font-size: 10vw;
  color: #fff;
  font-weight: 300;
  text-align: center;
  position: relative;
  width: 100%;
  margin: 0;
  letter-spacing: 0.12em;
}
</style>
