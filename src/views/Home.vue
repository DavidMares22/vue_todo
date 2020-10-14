<template>
  <div id="app">
    
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:tasks="todos" />
  
    <div class="center">
      {{previous}} | {{current}} | {{next}}
      <div class="pagination">
        <a v-on:click="getPreviousPage">❮</a>
        
        <a v-on:click="getNextPage">❯</a>
      </div>

    </div>
  

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
      todos: [],
      next:1,
      previous:1,
      current:1,
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

 getNextPage(){
            
            
            let self = this ;
            axios.get(`http://127.0.0.1:8085/api/v1/list/?page=${self.next}`)
        .then(function(res) {
          self.todos = res.data.results;
          self.current = res.data.pages.current;
          self.next = res.data.pages.current + 1;
          self.previous = res.data.pages.current - 1;
          
      })
      },
 getPreviousPage(){
            
            
            let self = this ;
            axios.get(`http://127.0.0.1:8085/api/v1/list/?page=${self.previous}`)
        .then(function(res) {
          self.todos = res.data.results;
          self.current = res.data.pages.current;
          self.next = res.data.pages.current + 1;
          self.previous = res.data.pages.current - 1;
          
      })
     
      },      
   
  },
    created() {
      let self = this ;
      axios.get('http://127.0.0.1:8085/api/v1/list/')
        .then(function(res) {
          self.todos = res.data.results;
          self.current = res.data.pages.current;
          self.next = res.data.pages.current + 1;
          self.previous = res.data.pages.current - 1;
          
      })
        // .then(res => this.todos = res.data.results )
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



.pagination {
  display: inline-block;
  
}
.center {
  
  text-align: center;
}

.pagination a {
  color: black;
  float: left;
  padding: 8px 16px;
  text-decoration: none;
  transition: background-color .3s;
  border: 1px solid #ddd;
}

.pagination a.active {
  background-color: #4CAF50;
  color: white;
  border: 1px solid #4CAF50;
}
</style>
