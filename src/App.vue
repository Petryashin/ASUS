<template>
  <header id="app">
    <TerminalMain />
  </header>
</template>

<script>
import TerminalMain from './components/TerminalMain.vue'

export default {
  name: 'App',
  components: {
    TerminalMain
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
