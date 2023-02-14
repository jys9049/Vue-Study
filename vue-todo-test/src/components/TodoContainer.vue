<template>
  <div class="todoContainer">
    <h1>Vue Todo-List</h1>
    <TodoInput v-on:addBtnClick="addTodo" />
    <TodoList :todo="todo" v-on:checked="checkedTodo" v-on:delete="deleteTodo"/>
  </div>
</template>

<script>
import TodoInput from './TodoInput.vue';
import TodoList from './TodoList.vue';

export default {
  components: {
    TodoInput,
    TodoList
  },
  data: function () {
    return {
      todo: [
        {
          id: 1,
          text: '뷰 공부하기',
          checked: false,
        },
        {
          id: 2,
          text: '넉스트 알아보기',
          checked: false,
        },
      ]
    }
  },
  methods: {
    addTodo(text) {
      if (this.todo.find(item => item.text === text) !== undefined) {
        return alert('이미 목록에 있습니다.')
      }
      this.todo.push({
        id: this.todo.length + 1,
        text: text,
        checked: false
      })
    },
    deleteTodo: function (id) {
      this.todo = this.todo.filter(item => item.id !== id)
    },
    checkedTodo: function (id) {
      const todoList = [...this.todo];
      const todoItem = todoList.find(item => item.id === id);

      if (todoItem) {
        todoItem.checked = !todoItem.checked
        this.todo = todoList
      }
    }
  },
  computed: {
    checkedText: function () {
      return this.todo.checked ? 'finishText' : null;
    }
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}

.todoContainer {
  display: flex;
  position: relative;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 350px;
  margin: 0 auto;
}

.inputContainer,
.todoItemContainer {
  display: flex;
  position: relative;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.todoItemContainer {
  flex-direction: column;
  margin-top: 10px;
}
</style>
