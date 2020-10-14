<template>
    <div class="todo-item" v-bind:class="{'is-complete':item.done}">
        <p>
            <input type="checkbox" v-on:change="markComplete(item)" :checked="item.done">
            {{item.title}}
            {{item.done}}
           
            <router-link class="view" v-bind:to="'/detail/'+item.id" >View</router-link>
        </p>
    </div>
     
</template>

<script>
import axios from 'axios';
export default {
    name: "TodoItem",
    props:["item"],
    methods:{
        markComplete(){
            this.item.done = !this.item.done;
      
      axios.put(`http://127.0.0.1:8085/api/v1/detail/${this.item.id}`, {
        'title': this.item.title,
        'done': this.item.done
    
       
      })

        }
    }
     
}
</script>

<style scoped>
.todo-item{
    color: #fff;
    background: #35495e;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}

.is-complete{
    text-decoration: line-through;
}



.view{
  background-color: #e7e7e7;
  border: none;
  color: black;
  padding: 5px 9px;
  text-align: center;
  text-decoration: none;
  float: right;
  font-size: 16px;
  cursor: pointer;
}

</style>