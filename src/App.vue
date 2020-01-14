<template>
  <div id="app">
    <Wiki />
  </div>
</template>

<script>
import Wiki from './components/Wiki.vue'

export default {
  name: 'app',
  components: {
    Wiki
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
