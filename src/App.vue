<template>
  <div id="app">
    <fs-calendar/>
  </div>
</template>

<script>
import FsCalendar from './components/FsCalendar'

export default {
  name: 'App',
  components: {
    FsCalendar
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
