<template>
  <div id="app">
    
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:tasks="todos" />
    
  </div>
</template>

<script>


import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo,

  },
  data(){
    return{
      todos: []
    }
  },
  methods:{
    
    addTodo(newTodo){
      // this.todos = [... this.todos,newTodo];
      
      const { title, completed } = newTodo;
      axios.post('http://127.0.0.1:8085/api/v1/list/', {
        title,
        completed,
       
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    },
   
  },
    created() {
      axios.get('http://127.0.0.1:8085/api/v1/list/')
        .then(res => this.todos = res.data)
        .catch(err => console.log(err));

        
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
