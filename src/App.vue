<template>
  <div class="app">
    <MenuButton class="menu-button" />
    <router-view/>
  </div>
</template>

<script>
import MenuButton from '@/components/MenuButton.vue'

export default {
  components: {
    MenuButton
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
  background: radial-gradient(#00003a, #000);
  background: radial-gradient(#0b1427, #0b101e);
  min-height: 100vh;
  display: flex;
}

.menu-button {
  position: fixed;
  top: 10px;
  right: 10px;
}
</style>
