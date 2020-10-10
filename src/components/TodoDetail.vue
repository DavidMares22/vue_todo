<template>
  <div class="details">
    <h1>Details</h1>
    <p>{{todo.title}}</p>
     <button class="del" @click="deleteTodo(todo.id)">X</button>
  </div>
</template>


<script>
import axios from 'axios';

export default {
    name: "TodoDetail",
    data(){
        return{
        todo: ''
        }
    },
    methods:{
        deleteTodo(id){
      // this.todos = this.todos.filter(todo => todo.id != id);
        axios.delete(`http://127.0.0.1:8085/api/v1/detail/${id}`);// eslint-disable-next-line 
           
    },        
        fetchTask(id){
             axios.get(`http://127.0.0.1:8085/api/v1/detail/${id}`)// eslint-disable-next-line 
        .then(res => this.todo =  res.data)
        .catch(err => console.log(err));   
        }
    },

    created(){
        this.fetchTask(this.$route.params.id);
    }
  
}
</script>

<style scoped>

.del{
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
</style>