<template>
    <div id="app">
      <Header/>
      <AddTodo v-on:add-todo="addTodo"/>
        <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" v-on:done-todo="doneTodo"/>
    </div>
</template>

<script>
  import Todos from './components/Todos';
  import AddTodo from './components/AddTodo';
  import axios from 'axios';
  import Header from './components/Header';
export default {
  name: 'App',
  components: {
   Todos,Header,AddTodo
  },
  data(){
    return {todos: [
      
    ]}
  },
  methods:{
    deleteTodo(id){
      axios.delete('https://jsonplaceholder.typicode.com/todos/${id}').then(this.todos = this.todos.filter(todo => todo.id !== id)).catch(err => console.log(err));
      
    },
    addTodo(todo){
      const {title, completed} = todo;
      axios.post('https://jsonplaceholder.typicode.com/todos', {title, completed}).then(res => this.todos = [...this.todos, res.data]).catch(err => console.log(err));

    },
   
  },
   created(){
      axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5').then(res => this.todos = res.data).catch(err => console.log(err))
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.btn{
  display: inline-block;
  border:none;
  background: #333;
  padding: 7px 20px;
  color: white;
  outline: none;
  cursor: pointer;
}
</style>
