<template>
    <div>
        <AddTodo v-on:addTodo="addTodo"/>
        <TodosList v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    </div>
</template>

<script>
import TodosList from '../components/TodosList.vue';
import AddTodo from '../components/AddTodo.vue';
import axios from 'axios';
export default {
  name: 'HomeView',
  components: {
    TodosList,
    AddTodo
},
data(){
  return{
    todos:[]
    // todos: [
    //   {
    //     id:1,
    //     title:"Todo One",
    //     completed:true
    //   },
    //     {
    //     id:2,
    //     title:"Todo Two",
    //     completed:false
    //   },
    //     {
    //     id:3,
    //     title:"Todo Three",
    //     completed:false
    //   }
    // ]
  }
},
methods:{
  deleteTodo(id){
    axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
    .then(this.todos = this.todos.filter(todo => todo.id !== id))
    .catch(err => console.log(err))
    
  },
  addTodo(newTodo){
    const {title, completed} = newTodo;
    axios.post('https://jsonplaceholder.typicode.com/todos', {
      title,
      completed
    })
    .then(res=> this.todos = [...this.todos,res.data])
    .catch(err => console.log(err))
  }
},
created(){
  axios.get('https://jsonplaceholder.typicode.com/todos?_limit=4')
  .then(res=> this.todos = res.data)
  .catch(err => console.log(err))
}
}
</script>

<style>
  body{
    font-family: Arial, Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
