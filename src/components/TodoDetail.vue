<template>
  <div class="container">
   
   <div class="container-btn">
       <button class="del" @click="deleteTodo(todo.id)">X</button> 
   </div>
    

  <form @submit.prevent="updateTodo(todo.id)">

    <label for="ftitle">Title</label>
    <div class="error" v-if="error">{{error}}</div>
    <input type="text" id="ftitle" name="title" v-model="todo.title">
    
     <input type="submit" value="Update">

  </form>

  

  </div>
</template>


<script>
import axios from 'axios';

export default {
    name: "TodoDetail",
    data(){
        return{
        todo: '',
        error:''
        }
    },
    methods:{
        deleteTodo(id){
      // this.todos = this.todos.filter(todo => todo.id != id);
      let self = this;
        axios.delete(`http://127.0.0.1:8085/api/v1/detail/${id}`)// eslint-disable-next-line 
        .then(function(res){
            self.$router.push({ name: 'Home' });
        });
    },        
        fetchTask(id){
             axios.get(`http://127.0.0.1:8085/api/v1/detail/${id}`)// eslint-disable-next-line 
        .then(res => this.todo =  res.data)
        .catch(err => console.log(err));   
        },
        
        updateTodo(id){
          let self = this;
          axios.put(`http://127.0.0.1:8085/api/v1/detail/${id}`, {
            'title':self.todo.title,
        
          
          }).then(function(){
                self.$router.push({ name: 'Home' });
          })
          .catch(function(err){
            
          if(err.response.data){

            // console.log(err.response.data.title);
            self.error = err.response.data.title[0];
          }

          // if (err.response) {
          //   console.log(err.response.data);
          //   console.log(err.response.status);
          //   console.log(err.response.headers);
          // } else if (err.request) {        
          //   console.log(err.request);
          // }
        });
            
          }        
    },

    created(){
        this.fetchTask(this.$route.params.id);
    }
  
}
</script>

<style scoped>

.container-btn{
    text-align: center;
}
.container {
  border-radius: 5px;
  background-color: #f2f2f2;
  padding: 20px;
 
}

.del{
    background: #ff0000;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
   
}

input[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}


input[type=text], select, textarea {
  width: 100%; /* Full width */
  padding: 12px; /* Some padding */ 
  border: 1px solid #ccc; /* Gray border */
  border-radius: 4px; /* Rounded borders */
  box-sizing: border-box; /* Make sure that padding and width stays in place */
  margin-top: 6px; /* Add a top margin */
  margin-bottom: 16px; /* Bottom margin */
  
}

.error {
 color: #ba3939;
  background: #ffe0e0;
  border: 1px solid #a33a3a;
}
</style>