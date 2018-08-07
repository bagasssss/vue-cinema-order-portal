<template>
  <div id="app">
    <cinema />
  </div>
</template>

<script>
import cinema from './components/cinema.vue'

export default {
  name: 'app',
  components: {
    cinema
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
