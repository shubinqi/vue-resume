<template>
  <div id="app">
    <ResumeName />
  </div>
</template>

<script>
import ResumeName from './components/ResumeName.vue'

export default {
  name: 'App',
  components: {
    ResumeName
  }
}
</script>

<style>
#app {
  max-width: 1200px;
  margin: 0 auto;
}
</style>
