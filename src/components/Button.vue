<template>
  <button
    class="button from-center"
    ref="button"
    @mouseenter="hover"
    @mouseleave="blur"
    @click="$emit('click')"
  >
    <div class="border" ref="border" />
    <div class="background" ref="background" />
    <slot />
  </button>
</template>

<script>
import { TimelineMax, Power4 } from 'gsap'

export default {
  name: 'Button',

  data () {
    return {
      tlButton: new TimelineMax({ paused: true })
    }
  },

  mounted () {
    this.tlButton
      .to(this.$refs.border, 0.5, { scaleX: 1, ease: Power4.easeOut }, 0)
      .to(this.$refs.background, 0.5, { scaleY: 1, ease: Power4.easeOut }, 0.2)
      .to(this.$refs.button, 0.5, { color: '#000', ease: Power4.easeOut }, 0.3)
  },

  methods: {
    hover () {
      this.tlButton.play()
    },

    blur () {
      this.tlButton.reverse()
    }
  }
}
</script>

<style scoped>
.button-wrap {
  position: relative;
  z-index: 1;
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
  letter-spacing: 0.7em;
  text-transform: uppercase;
  /* transition: all 500ms cubic-bezier(0.77, 0, 0.175, 1); */
  cursor: pointer;
  user-select: none;
}

.border,
.background {
  position: absolute;
  transition: inherit;
  z-index: -1;
  box-sizing: border-box;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
}

.button .border {
  border: 1px solid #fff;
  border-left: 0;
  border-right: 0;
  transform: scaleX(0);
}

.button .background {
  background: #fff;
  transform: scaleY(0);
  transform-origin: 50% 0%;
}
</style>
