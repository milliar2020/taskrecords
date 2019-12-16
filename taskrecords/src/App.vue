<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <TaskRecords msg="Welcome to Task Records Vue.js App"/>
  </div>
</template>

<script>
import TaskRecords from './components/TaskRecords.vue'

export default {
  name: 'app',
  components: {
    TaskRecords
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
