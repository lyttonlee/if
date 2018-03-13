<template>
  <div id="app">
    <img class="banner" :src="img">
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      img: 'http://fcfantasy.cn/fe2015/image/feif_bg.jpg'
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0 auto;
  width: 100%;
  max-width: 460px;
}
.banner {
  width: 100%;
}
</style>
