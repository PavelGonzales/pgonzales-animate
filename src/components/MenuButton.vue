<template>
  <button
    :class="['menu', 'reset-button', {'active': isActive}]"
    @click="toggleMenu"
    @mouseenter="play"
    @mouseleave="reverse"
  >
    <span class="dot first" />
    <span class="dot center" />
    <span class="dot last" />
    <div class="text">menu</div>
  </button>
</template>

<script>
import { TimelineLite } from 'gsap'

export default {
  name: 'HelloWorld',

  data () {
    return {
      isActive: false,
      tl: new TimelineLite({ paused: true })
    }
  },

  mounted () {
    this.tl
      .to('.first', { duration: 0.3, y: 0 }, 0)
      .to('.first', { duration: 0.3, x: -10, opacity: 0 }, 0.3)
      .to('.center', { duration: 0.3, opacity: 0 }, 0.3)
      .to('.last', { duration: 0.3, y: 0 }, 0)
      .to('.last', { duration: 0.3, x: 10, opacity: 0 }, 0.3)
      .fromTo('.text', { opacity: 0, scaleY: 0 }, { duration: 0.3, opacity: 1, scaleY: 1 }, 0.4)
  },

  methods: {
    toggleMenu () {
      this.isActive = !this.isActive
    },

    play () {
      this.tl.play()
    },

    reverse () {
      this.tl.reverse()
    }
  }
}
</script>

<style scoped>
.reset-button {
  border: none;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;

  background: transparent;

  /* inherit font & color from ancestor */
  color: inherit;
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
}

/* Remove excess padding and border in Firefox 4+ */
.reset-button::-moz-focus-inner {
  border: 0;
  padding: 0;
}

.menu {
  cursor: pointer;
  color: #fff;
  width: 42px;
  height: 42px;
}

.dot {
  width: 4px;
  height: 4px;
  border-radius: 50%;
  background-color: #fff;
  display: block;
  position: absolute;
  top: calc(50% - 2px);
  left: calc(50% - 2px);
}

.dot:nth-child(1) {
  transform: translate(0, -200%);
}

.dot:nth-child(3) {
  transform: translate(0, 200%);
}

.text {
  opacity: 0;
  position: absolute;
  top: 20%;
}
</style>
