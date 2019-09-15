<template>
  <div id="app">
  <!--<SliderOld/>
  <br>-->
  <Slider/>
  <br>
  </div>
</template>

<script>
// import SliderOld from './components/Slider_old'
import Slider from './components/Slider'
export default {
  name: 'App',
  components: {
    // SliderOld,
    Slider
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
