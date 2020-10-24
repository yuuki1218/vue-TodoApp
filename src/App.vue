<template>
  <div id="app">
    <TodoLists></TodoLists>
  </div>
</template>

<script>
import TodoLists from './views/TodoLists.vue';
export default {
  components: {
    TodoLists,
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

table {
  margin: 0 auto;
}

</style>
