<template>
  <div id="app">
    <img alt="Vue logo" class="brand" src="./assets/logo.png" />
    <ToDoList />
  </div>
</template>

<script>
import ToDoList from './components/TodoList.vue';

export default {
  name: "App",
  components: {
    ToDoList
  }
};
</script>

<!--<script>
import HelloWorld from "./components/HelloWorld.vue";

export default {
  name: "App",
  components: {
    HelloWorld
  }
};
</script>-->

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.brand {
  max-width: 100px;
}
</style>
