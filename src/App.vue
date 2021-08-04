<template>
  <user></user>
</template>

<script>
import user from './components/user.vue'

export default {
  name: 'App',
  components: {
    user
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
body{
  margin:0;
  padding:0;
  overflow-x: hidden;
}
</style>
