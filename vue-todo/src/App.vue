<template>
  <div id="app">
    <TodoHeader />
    <TodoInput />
    <TodoList />
    <TodoFooter />

  </div>
</template>

<script>

import TodoFooter from './components/TodoFooter.vue'
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoHeader from './components/TodoHeader.vue';

export default {
  name: 'App',
  components: {
    TodoFooter,
    TodoHeader,
    TodoInput,
    TodoList,
  }
}
</script>

<style>
body {
  text-align: center;
  background-color: #F6F6F6;
}

input {
  border-style: groove;
  width: 200px;
}

button {
  border-style: groove;
}

.shadow {
  box-shadow: 5px 10px 10px rgba(0, 0, 0, .3);
}
</style>
