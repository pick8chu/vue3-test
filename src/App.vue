<template>
  <img class="img" alt="Vue logo" src="./assets/logo.png">
  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  
  
  <!-- <Suspense timeout="0">
    <fallback-test/>
  </Suspense> -->

  <!-- <play-ground/> -->

  <window-popup-test/>

</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
// import fallbackTest from './components/fallbackTest.vue'
// import playGround from './components/playground.vue'
import windowPopupTest from './components/windowPopupTest.vue'

export default {
  name: 'App',
  components: {
    // HelloWorld,
    // fallbackTest,
    // playGround,
    windowPopupTest
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
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
  margin-left: 60px;
}
.img {
  text-align: center;
  width: 60px;
  height: 60px;
}
</style>
