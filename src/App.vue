<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  
  
  <!-- <Suspense timeout="0">
    <fallback-test/>
  </Suspense> -->

  <play-ground/>
  
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import fallbackTest from './components/fallback-test.vue'
import playGround from './components/playground.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // fallbackTest,
    playGround
  },
  setup(){
    return null
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
