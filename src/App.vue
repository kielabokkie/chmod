<template>
  <div id="app">
    <chmod></chmod>
  </div>
</template>

<script>
import Chmod from './components/Chmod'

export default {
  components: {
    Chmod
  }
}
</script>

<style>
html {
  height: 100%;
  background: #0299A5;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  margin: 0;
  padding: 0;
}

#app {
  color: #fff;
  margin-top: -100px;
  max-width: 600px;
  font-family: 'Ubuntu', Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}
</style>
