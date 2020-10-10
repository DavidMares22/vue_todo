<template>
  <div class="details">
    <h1>Details</h1>
    <p>{{todo.title}}</p>
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
        fetchTask(id){
             axios.get(`https://jsonplaceholder.typicode.com/todos/${id}`)// eslint-disable-next-line 
        .then(res => this.todo =  res.data)
        .catch(err => console.log(err));   
        }
    },

    created(){
        this.fetchTask(this.$route.params.id);
    }
  
}
</script>