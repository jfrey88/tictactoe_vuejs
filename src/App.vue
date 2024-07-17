<template>
  <img alt="Vue logo" src="./assets/photo bleu.jpg">
  <HelloWorld msg="TIC TAC TOE"/>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
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
img{
  max-width: 150px;
  max-height: 150px;
  border-radius: 150px;
}
</style>
