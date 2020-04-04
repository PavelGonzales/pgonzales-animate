<template>
  <div class="app">
    <div class="border" ref="border" />
    <VideoBackground
      v-for="(sources, index) in videos"
      :key="`video-${index}`"
      :sources="sources"
    />

    <h1 class="title" ref="title">Pavel Gonzales</h1>
    <button
      class="button from-center"
      ref="button"
    >
      Read resume
    </button>
  </div>
</template>

<script>
/* eslint-disable */
import { TimelineMax, TweenLite, Linear, Power4 } from 'gsap'
import VideoBackground from '@/components/VideoBackground.vue'

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
    VideoBackground
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

.button {
  border: none;
  margin: 0;
  width: auto;
  overflow: visible;
  /* inherit font & color from ancestor */
  font: inherit;
  /* Normalize `line-height`. Cannot be changed from `normal` in Firefox 4+. */
  line-height: normal;
  /* Corrects font smoothing for webkit */
  -webkit-font-smoothing: inherit;
  -moz-osx-font-smoothing: inherit;
  /* Corrects inability to style clickable `input` types in iOS */
  -webkit-appearance: none;
  text-align: inherit;
  outline: none;
  border-radius: 0;

  background-color: transparent;
  font-weight: 600;
  box-sizing: border-box;

  position: relative;	
	padding: 1.4rem 4.2rem;
	padding-right: 3.1rem;
	font-size: 1.4rem;
	color: #fff;
	letter-spacing: 1.1rem;
	text-transform: uppercase;
	transition: all 500ms cubic-bezier(0.77, 0, 0.175, 1);	
	cursor: pointer;
	user-select: none;
}

.button:before, .button:after {
	content: '';
	position: absolute;	
	transition: inherit;
	z-index: -1;
}

.button:hover {
	color: var(--def);
	transition-delay: .5s;
}

.button:hover:before {
	transition-delay: 0s;
}

.button:hover:after {
	background: #fff;
	transition-delay: .35s;
}

/* From center */

.from-center:before {
	top: 0;
	left: 50%;
	height: 100%;
	width: 0;
	border: 1px solid #fff;
	border-left: 0;
	border-right: 0;
}

.from-center:after {
	bottom: 0;
	left: 0;
	height: 0;
	width: 100%;
	background: #fff;
}

.from-center:hover:before {
	left: 0;
	width: 100%;
}

.from-center:hover:after {
	top: 0;
	height: 100%;
}

body {
	--def: #96B7C4; 	
	--inv: #fff;
}
</style>
