<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo"/>
     <FilterTodos /> 
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>  
    
  </div>
</template>
 
<script>
import Todos from '../components/Todos';
import Header from '../components/layout/header';
import AddTodo from '../components/AddTodo';
import FilterTodos from '../components/FiltersTodo';
import axios from 'axios';


export default { 
  name: 'Home',
  components: {
    Todos,
    Header,
    AddTodo,
    FilterTodos
  },
   data() {
    return {
      todos: []
    }
  },
   created() {
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')
        .then(res=> this.todos =  res.data)
        .catch(err=>console.log(err));
    },
  methods: {
    deleteTodo(id) {
      this.todos = this.todos.filter(x=>x.id !== id);
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      }).then(res=>this.todos = [...this.todos,res.data])
      .catch(err=>console.log(err));
     
    }
  }  
  }

</script>

<style>
* {
 box-sizing: border-box;
 margin:0;
 padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display: inline-block;
  border:none;
  background: #555;
  color:#fff;
  padding:7px 20px;
  cursor: pointer;
}
</style>
