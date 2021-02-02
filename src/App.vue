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
  import Header from './components/Header';
export default {
  name: 'App',
  components: {
   Todos,Header,AddTodo
  },
  data(){
    return {todos: [
      {
        id: 1,
        title: "Todo One",
        completed: false,
      },{
        id: 2,
        title: "Todo Two",
        completed: false,
      },{
        id: 3,
        title: "Todo Three",
        completed: false,
      }
    ]}
  },
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(todo){
      this.todos = [...this.todos, todo];
    }
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
