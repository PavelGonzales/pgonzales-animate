<template>
  <div ref="menu" :class="['menu', {'hidden': !value}]">
    <div class="overlay" ref="overlay">
      <div class="overlay-background" ref="overlay-background" />
      <div class="overlay-part overlay-top" ref="overlay-top" />
      <div class="overlay-part overlay-bottom" ref="overlay-bottom" />
    </div>

    <nav class="nav" ref="nav" @mousemove="moveNav">
      <ul class="list" ref="list">
        <li
          v-for="item in menuItems"
          :key="item.text"
          class="list-item"
          ref="list-item"
        >
          <router-link
            class="list-link"
            :to="item.href"
            :data-text="item.text"
            @click.native="close"
          >
              {{ item.text }}
          </router-link>
        </li>
      </ul>
    </nav>
    <button class="close-button" @click="close">
      close
    </button>
  </div>
</template>

<script>
/* eslint-disable */
import { TimelineMax, TweenLite, Linear, Power4 } from 'gsap'

export default {
  name: 'Menu',

  data () {
    return {
      tl: new TimelineMax({
        paused: true,
        onReverseComplete: () => this.$emit('input', false)
      }),
      menuItems: [
        {
          href: '/about',
          text: 'About'
        },
        {
          href: '/experience',
          text: 'Experience'
        },
        {
          href: '/skills',
          text: 'Skills'
        },
        {
          href: '/contacts',
          text: 'Contacts'
        }
      ]
    }
  },

  props: {
    value: {
      type: Boolean,
      required: true
    }
  },

  mounted () {
    const speed = 0.6 // sec
    this.tl
      .from(this.$refs.nav, speed, { opacity: 0, scale: 2, ease: Power4.easeOut }, 0)
      .from(this.$refs['overlay-top'], speed, { y: -this.$refs['overlay-top'].clientHeight, ease: Power4.easeOut }, 0)
      .from(this.$refs['overlay-bottom'], speed, { y: this.$refs['overlay-bottom'].clientHeight, ease: Power4.easeOut }, 0)
      .from(this.$refs['overlay-background'], speed, { opacity: 0, ease: Power4.easeOut }, 0)
  },

  watch: {
    value (value) {
      if (value) {
        this.play()
      }
    }
  },

  methods: {
    moveNav (e) {
      // 0 - 1325
      const soot = (this.$refs.list.clientWidth - window.innerWidth) / window.innerWidth
      const xPos = -(e.clientX * soot)

      console.log('xPos: ', xPos)
      console.log({clientWidth: this.$refs.list.clientWidth, clientX: e.clientX, soot})
      TweenLite.to(this.$refs.list, 1, { x: xPos })
    },

    close () {
      this.reverse()
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
.menu {
  width: 100vw;
  height: 100vh;
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  z-index: 100;
}

.hidden {
  opacity: 0;
  visibility: hidden;
}

.overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.overlay-background {
  background-color: rgb(0, 0, 34);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.overlay-part {
  position: relative;
  height: 50vh;
}

.overlay-top {
  position: relative;
  background: linear-gradient(0deg, rgba(0, 0, 34, 0) 0%, rgb(0, 0, 0) 100%);
}

.overlay-bottom {
  position: relative;
  background: linear-gradient(0deg, rgb(0, 0, 0) 0%, rgba(0, 0, 34, 0) 100%);
}

.nav {
  width: 100%;
  display: flex;
}

.list {
  list-style: none;
  display: inline-flex;
  padding: 0 50vw;
  transform: translateX(-50vw);
}

.list-item {
  padding: 4px 16px;
  margin: 0 100px;
}

.close-button {
  position: fixed;
  top: 10px;
  right: 10px;
}

.list-link {
  text-decoration: none;
  color: #fff;
  font-size: 100px;
  text-transform: uppercase;
  font-weight: 800;
  position: relative;
  opacity: 0.5;
}

.list-link:hover {
  opacity: 1;
}

.list-link:hover::before,
.list-link:hover::after {
  display: block;
}

.list-link::before,
.list-link::after {
  color: white;
  content: attr(data-text);
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: hidden;
  top: 0;
  display: none;
}

.list-link::before {
  left: 3px;
  text-shadow: -2px 0 red;
  animation-name: glitch-animation-1;
  animation-duration: 2s;
  animation-timing-function: linear;
  animation-delay: 0s;
  animation-iteration-count: infinite;
  animation-direction: reverse-alternate;
}

.list-link::after {
  left: -3px;
  text-shadow: -2px 0 blue;
  animation-name: glitch-animation-2;
  animation-duration: 2s;
  animation-timing-function: linear;
  animation-delay: 0s;
  animation-iteration-count: infinite;
  animation-direction: reverse-alternate;
}

@keyframes glitch-animation-1 {
  0% {
    clip: rect(125px, 650px, 42px, 0px);
  }

  5% {
    clip: rect(81px, 650px, 92px, 0px);
  }

  10% {
    clip: rect(106px, 650px, 54px, 0px);
  }

  15% {
    clip: rect(13px, 650px, 139px, 0px);
  }

  20% {
    clip: rect(22px, 650px, 48px, 0px);
  }

  25% {
    clip: rect(48px, 650px, 32px, 0px);
  }

  30% {
    clip: rect(29px, 650px, 80px, 0px);
  }

  35% {
    clip: rect(86px, 650px, 98px, 0px);
  }

  40% {
    clip: rect(5px, 650px, 131px, 0px);
  }

  45% {
    clip: rect(6px, 650px, 43px, 0px);
  }

  50% {
    clip: rect(82px, 650px, 41px, 0px);
  }

  55% {
    clip: rect(105px, 650px, 30px, 0px);
  }

  60% {
    clip: rect(61px, 650px, 140px, 0px);
  }

  65% {
    clip: rect(65px, 650px, 30px, 0px);
  }

  70% {
    clip: rect(130px, 650px, 72px, 0px);
  }

  75% {
    clip: rect(39px, 650px, 14px, 0px);
  }

  80% {
    clip: rect(97px, 650px, 102px, 0px);
  }

  85% {
    clip: rect(118px, 650px, 100px, 0px);
  }

  90% {
    clip: rect(99px, 650px, 90px, 0px);
  }

  95% {
    clip: rect(16px, 650px, 53px, 0px);
  }

  100% {
    clip: rect(54px, 650px, 126px, 0px);
  }
}

@keyframes glitch-animation-2 {
  0% {
    clip: rect(126px, 650px, 48px, 0px);
  }

  5% {
    clip: rect(83px, 650px, 73px, 0px);
  }

  10% {
    clip: rect(60px, 650px, 78px, 0px);
  }

  15% {
    clip: rect(149px, 650px, 101px, 0px);
  }

  20% {
    clip: rect(113px, 650px, 150px, 0px);
  }

  25% {
    clip: rect(34px, 650px, 44px, 0px);
  }

  30% {
    clip: rect(103px, 650px, 67px, 0px);
  }

  35% {
    clip: rect(35px, 650px, 106px, 0px);
  }

  40% {
    clip: rect(35px, 650px, 26px, 0px);
  }

  45% {
    clip: rect(105px, 650px, 15px, 0px);
  }

  50% {
    clip: rect(4px, 650px, 148px, 0px);
  }

  55% {
    clip: rect(138px, 650px, 141px, 0px);
  }

  60% {
    clip: rect(35px, 650px, 143px, 0px);
  }

  65% {
    clip: rect(136px, 650px, 60px, 0px);
  }

  70% {
    clip: rect(78px, 650px, 55px, 0px);
  }

  75% {
    clip: rect(16px, 650px, 110px, 0px);
  }

  80% {
    clip: rect(149px, 650px, 78px, 0px);
  }

  85% {
    clip: rect(133px, 650px, 58px, 0px);
  }

  90% {
    clip: rect(80px, 650px, 98px, 0px);
  }

  95% {
    clip: rect(3px, 650px, 50px, 0px);
  }

  100% {
    clip: rect(29px, 650px, 69px, 0px);
  }
}
</style>
