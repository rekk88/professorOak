<template>
  <div id="app">
    <Home />
  </div>
</template>


<script>
import Home from './components/Home.vue'

export default {
  name: 'App',

  components: {
    Home
  }
}
</script>


<style lang="scss">
@import 'scss/commons.scss';
@import 'scss/colors.scss';
@import 'scss/type.scss';


#app {
  // font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
