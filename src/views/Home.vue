<template>
  <div class="home">
    <h1 class="title">Pavel Gonzales</h1>
  </div>
</template>

<script>

export default {
  name: 'Home'
}
</script>

<style scoped>
.home {
  margin: auto;
}

.title {
  font-size: 10vw;
  color: #D3D3D3;
  font-weight: 300;
  text-align: center;
  background: linear-gradient(to right, #D3D3D3 20%, #C0C0C0 40%, #C0C0C0 60%, #D3D3D3 80%);
  background-size: 200% auto;
  background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: textShine 8s ease-in-out infinite;
}

@keyframes textShine {
  to {
    background-position: 200%;
  }
}
</style>
