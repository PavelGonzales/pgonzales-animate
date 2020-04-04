<template>
  <div class="root">
    <div class="overlay" ref="overlay" />
    <video autoplay muted loop ref="video">
      <source
        v-for="source in sources"
        :key="source.src"
        :src="source.src"
        :type="source.type"
      >
      Your browser does not support the video tag.
    </video>
  </div>
</template>

<script>
import { TimelineMax, Power4 } from 'gsap'

export default {
  name: 'VideoBackground',

  data () {
    return {
      tlEntry: new TimelineMax({ paused: true })
    }
  },

  mounted () {
    this.tlEntry
      .from(this.$refs.overlay, 3, { opacity: 0, ease: Power4.easeOut }, 1.5)

    setTimeout(() => {
      this.tlEntry.play()
    }, 300)
  },

  props: {
    sources: {
      type: Array,
      default: () => []
    }
  }
}
</script>

<style scoped>
.root {
  width: 100vw;
  height: 100vh;
  overflow: hidden;
  position: fixed;
}

video, source {
  height: 100%;
  width: 177.77777778vh; /* 100 * 16 / 9 */
  min-width: 100%;
  min-height: 56.25vw; /* 100 * 9 / 16 */
  position: absolute;
  left: 50%; /* % of surrounding element */
  top: 50%;
  transform: translate(-50%, -50%); /* % of current element */
}

.overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: #000;
  opacity: 0.3;
  z-index: 1;
}
</style>
