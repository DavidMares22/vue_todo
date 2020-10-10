<template>
    <div class="todo-item" v-bind:class="{'is-complete':item.completed}">
        <p>
            <input type="checkbox" v-on:change="markComplete">
            {{item.title}}
            {{item.id}}
           
            <router-link class="view" v-bind:to="'/detail/'+item.id" >View</router-link>
        </p>
    </div>
     
</template>

<script>
export default {
    name: "TodoItem",
    props:["item"],
    methods:{
        markComplete(){
            this.item.completed = !this.item.completed;
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