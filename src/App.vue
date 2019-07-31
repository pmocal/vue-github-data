<template>
  <div id="app">
    <github-input></github-input>
    <github-output></github-output>
  </div>
</template>

<script>
import GithubInput from './components/GithubInput.vue'
import GithubOutput from './components/GithubOutput.vue'

export default {
  name: 'app',
  components: {
    GithubInput,
    GithubOutput
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
