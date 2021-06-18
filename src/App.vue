<template>
  <h style="font-size: 100px;">Color Game</h>
  <Box/>
</template>

<script>
import Box from './components/Box.vue'

export default {
  name: 'App',
  components: {
    Box
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
  margin-top: 40px;
}

html{
  background: #21B6A8;
}
</style>
