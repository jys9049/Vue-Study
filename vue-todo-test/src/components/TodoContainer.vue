<template>
    <div class="todoContainer">
      <h1>Vue Todo-List</h1>
      <InputContainer/>
      <div class="todoItemContainer">
          <li class="todoItem" v-for="item in todo" :key="item.id">
            <input type="checkbox" name="check" id="check" v-on:click="checkedTodo(item.id)" v-bind:checked="item.checked"/>
            <h3 v-bind:class="{'finishText': item.checked}" >{{ item.text }}</h3>
            <button v-on:click="deleteTodo(item.id)"> X </button>
          </li>
        </div>
    </div>
  </template>
  
  <script>
import InputContainer from './InputContainer.vue';

  export default {
    components: {
        'InputContainer': InputContainer
    },
    data: function() {
      return {
        text: '',
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
      addTodo: function() {
        if(this.todo.find(item => item.text === this.text) !== undefined) {
          this.text = '';
          return alert('이미 목록에 있습니다.')
        }
  
        if(this.text.match(/\s/g) || this.text === '') {
          return this.text = ''
        }
  
        this.todo.push({
          id: this.todo.length + 1,
          text: this.text,
          checked: false
        })
        this.text = '';
      },
      deleteTodo: function(id) {
        this.todo = this.todo.filter(item => item.id !== id)
      },
      checkedTodo: function(id) {
        const todoList = [...this.todo];
        const todoItem = todoList.find(item => item.id === id);
  
        if(todoItem) {
          todoItem.checked = !todoItem.checked
          this.todo = todoList
        }
      }
    },
    computed: {
      checkedText: function() {
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
    
    .inputContainer, .todoItemContainer {
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
  
    .inputContainer > input {
      width: 100%;
      height: 40px;
      border: 1px solid #c9c9c9;
      padding-left: 10px;
    }
  
    .inputContainer > button {
      position: absolute;
      right: 15px;
      width: 30px;
      height: 30px;
      background: white;
      border: none;
      cursor: pointer;
    }
  
    li {
      display: flex;
      align-items: center;
      justify-content: space-between;
      width: 100%;
      list-style: none;
    }
  
    li > input[type="checkbox"] {
      width: 25px;
      height: 25px;
      border: 1px solid #c9c9c9;
      margin: 0;
    }
  
    li > button {
      width: 25px;
      height: 25px;
      background: white;
      border: 1px solid #c9c9c9;
      border-radius: 4px;
    }
  
    .finishText {
      color:red;
    }
  </style>
  