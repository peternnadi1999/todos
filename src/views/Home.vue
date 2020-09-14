<template>
  <div id="app">
    <addTodo v-on:add-Todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
    
  </div>
</template>

<script>
import addTodo from '../components/addTodo';
import Todos from '../components/Todos';
import axios from 'axios'

export default {
  name: 'Home',
  components: {
    addTodo,
    Todos

  },
  data(){
    return{
      todos:[
        {
          id:1,
          title:"todos one",
          completed:true
        }
      ]
    }
   
    
  },
  methods:{
    deleteTodo(id){
      
      this.todos = this.todos.filter(todo => todo.id !==id);
    },

    
    addTodo(newTodo){
      const {title ,completed}= newTodo;

        axios.post('https://jsonplaceholder.typicode.com/todos',{
          title,
          completed
        })
     .then(res => this.todos = [...this.todos, res.data])
     .catch(err => console.log(err))

    }
  },
  
  created(){
     axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
     .then(res => this.todos = res.data)
     .catch(err => console.log(err))
  }

}
</script>

<style>
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body{
  line-height: 1.4;
  font-family: Arial, Helvetica, sans-serif;
}
</style>
