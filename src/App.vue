<template>
  <div id="app">
    <slider></slider>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Slider from './components/slider.vue'

export default {
  name: 'App',
  components: {
    'Slider': () => import('./components/slider.vue')
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
