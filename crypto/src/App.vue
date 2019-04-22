<template>
  <div id="app">

    <Crypto/>
  </div>
</template>

<script>
import Crypto from './components/CCAPIExample'

export default {
  name: 'app',
  components: {
    Crypto
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
