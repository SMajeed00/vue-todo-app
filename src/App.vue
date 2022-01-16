<template>
  <div id="app">
    <appTodo></appTodo>
  </div>
</template>

<script>
import Todo from './components/TodoApp.vue'

export default {
  name: 'App',
  components: {
    appTodo: Todo
  }
}
</script>

<style>
</style>
