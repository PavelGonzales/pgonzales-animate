<template>
  <div class="app">
    <MenuButton class="menu-button" @toggle="toggleMenu" />
    <Menu v-model="isOpenMenu" />
    <router-view/>
  </div>
</template>

<script>
import MenuButton from '@/components/MenuButton.vue'

export default {
  components: {
    MenuButton,
    Menu: () => import('@/components/Menu.vue')
  },

  data () {
    return {
      isOpenMenu: false
    }
  },

  methods: {
    toggleMenu (value) {
      this.isOpenMenu = value
    }
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
  background: radial-gradient(rgb(0, 0, 30), rgb(0, 0, 0));
  /* background: radial-gradient(#0b1427, #0b101e); */
  min-height: 100vh;
  display: flex;
}

.menu-button {
  position: fixed;
  top: 10px;
  right: 10px;
}
</style>
