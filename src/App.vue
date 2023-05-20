<template>
  <div id="app">
    <TodoManager msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import TodoManager from './components/TodoManager.vue'

export default {
  name: 'App',
  components: {
    TodoManager
  }
}
</script>

<style>
</style>
