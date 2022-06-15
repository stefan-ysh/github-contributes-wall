<template>
  <div id="app">
    <GithubWall />
  </div>
</template>

<script>
import GithubWall from './components/GithubWall.vue'

export default {
  name: 'App',
  components: {
    GithubWall
  }
}
</script>

<style lang="less">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
