<template>
  <div id="app">
    <info-page v-show="showinfo" />
    <div>
      <h1>Cycles</h1>
      <h1>{{startcycle}}</h1>
    <!-- <HelloWorld  /> -->
    <h1>Budget Pomodoro Clock</h1>
    <timer @addcycle="startcycle+=1" @resetcycles="startcycle = 0" />
    </div>
    <button id="how2use" @click="showinfo = !showinfo">How to use</button>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Timer from './components/Timerblock.vue'
import InfoPage from './components/InfoPage.vue'

export default {
  name: 'App',
  created () {
            document.title = "Budget Pomodoro Clock";
        },
  components: {
    // HelloWorld,
    Timer,
    InfoPage
  },
  data() {
    return {
      startcycle:0,
      showinfo:false
    }
  }
}
</script>

<style>
/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
} */
#app {
display: flex;
  align-items: center;
  justify-content: space-between;
  flex-direction: column;
  min-height: 100vh;
  text-align: center;
  
  
}
html, body{
  min-height: 100vh;
  margin: 0;
  padding: 0;
  width: 100%;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -webkit-tap-highlight-color: rgba(0,0,0,0);
  background-color: #2c3e50;
  color: #42b983;
}
#how2use {
  margin-bottom: 5%;
  z-index: 1;
}
</style>
