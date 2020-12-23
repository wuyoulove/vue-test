<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <video1 />
    <video3 />
    <video5 /> -->
    <draggable />
    <!-- <vuedraggable /> -->
    <!-- <draggableTest1 /> -->
    <!-- <jqueryDraggable /> -->
  </div>
</template>

<script>
import video1 from './components/01-video.vue'
import video3 from './components/03-video.vue'
import video5 from './components/05-video.vue'
import draggable from './components/draggable.vue'
import vuedraggable from './components/vuedraggable.vue'
import draggableTest1 from './components/draggableTest1.vue'
import jqueryDraggable from './components/jqueryDraggable.vue'

export default {
  name: 'app',
  components: {
    video1,
    video3,
    video5,
    draggable,
    vuedraggable,
    draggableTest1,
    jqueryDraggable
  }
}
</script>

<style>
html,body{
  width: 100%;
  height: 100%;
}
*{
  margin: 0;
  padding: 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 100%;
  height: 100%;
}
</style>
