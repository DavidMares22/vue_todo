<template>
  <div id="app">
    <Header />
    <AddTodo />
    <Todos v-bind:tasks="todos" v-on:del-todo="deleteTodo" />
    
  </div>
</template>

<script>

import Header from './components/layout/header'
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'

export default {
  name: 'App',
  components: {
    Todos,
    Header,
    AddTodo,

  },
  data(){
    return{
      todos: [
        {
          id: 1,
          title: "Todo One",
          completed: false
        },
        {
          id: 2,
          title: "Todo Two",
          completed: false
        },
        {
          id: 3,
          title: "Todo Three",
          completed: false
        }        
      ]
    }
  },
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id);
    }
  }
}
</script>

<style>

*{
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border: none;
  background: rgb(3, 157, 184);
  color: #fff;
  padding: 7px 20px;
  cursor:pointer;
}

.btn:hover{
  background: rgb(12, 12, 12);
}

</style>
