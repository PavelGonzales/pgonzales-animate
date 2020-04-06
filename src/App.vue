<template>
  <div class="app">
    <div class="cursor" ref="cursor" />
    <div class="border" ref="border">
      <div class="border-top" ref="border-top" />
      <div class="border-bottom" ref="border-bottom" />
      <div class="border-left" ref="border-left" />
      <div class="border-right" ref="border-right" />
    </div>
    <VideoBackground
      v-for="(sources, index) in videos"
      :key="`video-${index}`"
      :sources="sources"
    />

    <h1 class="title" ref="title">Pavel Gonzales</h1>
    <div ref="button">
      <Button @click="openResume">About</Button>
    </div>
    <div class="resume-wrap" ref="resumeWrap">
      <Resume @close="closeResume" />
    </div>
  </div>
</template>

<script>
/* eslint-disable */
import { TimelineMax, TweenLite, Linear, Power4 } from 'gsap'
import VideoBackground from '@/components/VideoBackground.vue'
import Button from '@/components/Button.vue'
import Resume from '@/components/Resume.vue'

export default {
  mounted () {
    TweenLite.set(this.$refs.cursor, {
      xPercent: -50,
      yPercent: -50
    });

    window.addEventListener("mousemove", this.moveCircle);

    const borderSizeY = window.innerHeight / 25 / 2
    const borderSizeX = window.innerWidth / 25 / 2
    const borderScaleX = window.innerWidth / (window.innerWidth - 30)
    const borderScaleY = window.innerHeight / (window.innerHeight - 30)
    const speed = 2 // sec

    this.tlEntry
      .from(this.$refs['border-top'], speed, { y: -15, scaleY: borderSizeY, scaleX: borderScaleX, ease: Power4.easeOut }, 0)
      .from(this.$refs['border-bottom'], speed, { y: 15, scaleY: borderSizeY, scaleX: borderScaleX, ease: Power4.easeOut }, 0)
      .from(this.$refs['border-left'], speed, { x: -15, scaleX: borderSizeX, scaleY: borderScaleY, ease: Power4.easeOut }, 0)
      .from(this.$refs['border-right'], speed, { x: 15, scaleX: borderSizeX, scaleY: borderScaleY, ease: Power4.easeOut }, 0)

      .from(this.$refs.title, 3, { opacity: 0, y: -20, ease: Power4.easeOut }, 1.5)
      .from(this.$refs.button, 3, { opacity: 0, y: 30, ease: Power4.easeOut }, 1.5)

    this.tlResume
      // .to(this.$refs['border-top'], speed, { scaleY: borderSizeY, ease: Power4.easeOut }, 0)
      .to(this.$refs['border-bottom'], 1.3, { scaleY: (window.innerHeight - 30) / 25, ease: Power4.easeOut }, 0)
      // .to(this.$refs['border-left'], speed, { scaleX: borderSizeX, ease: Power4.easeOut }, 0)
      // .to(this.$refs['border-right'], speed, { scaleX: borderSizeX, ease: Power4.easeOut }, 0)
      .to(this.$refs.title, 1, { opacity: 0, y: -20, ease: Power4.easeOut }, 0)
      .to(this.$refs.button, 1, { opacity: 0, y: 30, ease: Power4.easeOut }, 0)
      .from(this.$refs.resumeWrap, 1, { autoAlpha: 0, y: 30 }, 0.5)

    setTimeout(() => {
      this.tlEntry.play()
    }, 300) 
  },

  data () {
    return {
      tlEntry: new TimelineMax({ paused: true }),
      tlResume: new TimelineMax({ paused: true }),
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
    Button,
    Resume
  },

  methods: {
    openResume () {
      console.log('openResume')
      this.tlResume.play()
    },

    closeResume () {
      console.log('closeResume')
      this.tlResume.reverse()
    },

    moveCircle(e) {
      TweenLite.to(this.$refs.cursor, 0.3, {
        x: e.clientX,
        y: e.clientY
      });
    }
  }
}
</script>
<style>
body {
  font-family: 'Cormorant Infant', serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0;
}

* {
  cursor: none;
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
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  pointer-events: none;
}

.border-top,
.border-bottom,
.border-left,
.border-right {
  position: absolute;
  background-color: #fff;
}

.border-top,
.border-bottom {
  height: 25px;
  width: calc(100% - 30px);
  left: 15px;
}

.border-left,
.border-right {
  width: 25px;
  height: calc(100% - 30px);
  top: 15px;
}

.border-top {
  top: 15px;
  transform-origin: top center;
}

.border-bottom {
  bottom: 15px;
  transform-origin: bottom center;
  z-index: 1;
}

.border-left {
  left: 15px;
  transform-origin: center left;
}

.border-right {
  right: 15px;
  transform-origin: center right;
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

.resume-wrap {
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  z-index: 1;
}

.cursor {
  position: fixed;
  top: 0;
  left: 0;
  pointer-events: none;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  background-color: #fff;
  border: 2px solid #000;
  z-index: 1000;
  opacity: 0.5;
}
</style>
