<template>
  <div id="app">
    <vote></vote>
  </div>
</template>

<script>
import Vote from './components/Vote'

export default {
  name: 'app',
  components: {
    Vote
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
}
</style>
