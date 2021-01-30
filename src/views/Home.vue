<template>
  <div id="app">
    <Header/>
    <Search v-on:input="handleSearch(input)"/>
    <AddTodo v-on:add-todo="addTodo"/>
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
import axios from "axios";
import Search from "../components/Search"

export default {
  name: 'Home',
  components: {
    Todos,
    AddTodo,
    Search
  },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then( this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => console.log(err))
      
    },
    addTodo(newTodo) {
      const {title, completed} = newTodo
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title, 
        completed
      })
      .then(resp => this.todos = [...this.todos, resp.data])
      .catch(err => console.log(err))
      
    }
  },
    computed: {
    handleSearch() {
      return this.todos.filter((todo) => {
        return todo.title.toLowerCase().includes(this.input.toLowerCase());
      });
    },
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5 ')
    .then(resp => this.todos = resp.data)
    .catch(err => console.log(err))
  }
}
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn {
  display: inline-block;
  border: none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover {
  background: #666;
}
</style>
