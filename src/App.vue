<template>
  <div>
    <div id="header">
      <SearchTodo v-on:query-change="querySearch" />
    </div>

    <div id="main-container">
      <h2>Todos</h2>
      <TodoAdd v-on:add-todo="addTodo" />
      <Todos v-bind:todoslist="copyTodos" v-on:delete-todo="deleteTodo"/>
    </div>
  </div>
</template>

<script>
import SearchTodo from './components/SearchTodo.vue'
import Todos from './components/Todos.vue'
import TodoAdd from './components/TodoAdd.vue'

export default {
  name: 'App',
  components: {
    Todos,
    TodoAdd,
    SearchTodo
  },
  methods:{
    deleteTodo(id){
      this.todos = this.todos.filter(todo => todo.id != id)
      this.copyTodos = [...this.todos]
    },
    addTodo(todo){
      this.todos.push(todo)
      this.copyTodos = [...this.todos]
    },
    querySearch(query){
      if(query.trim() === ''){
        this.copyTodos = [...this.todos]
      } else {
        const temp = this.todos.filter(todo => {
          return todo.title.toUpperCase().includes(query.toUpperCase())
        });
        this.copyTodos = [...temp]
      }
    }
  },
  data(){
    return{
      todos: [
        {
          id: 0,
          title: 'Comprar la cena',
          completed: false
        },
        {
          id: 1,
          title: 'Sacar al perro',
          completed: true
        },
        {
          id: 2,
          title: 'Estudiar',
          completed: false
        },
        {
          id: 3,
          title: 'Terminar Test',
          completed: true
        }
      ],
      copyTodos: []
    }
  },
  created(){
    this.copyTodos = [...this.todos]
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    font-size: 1.5em;
    padding: 0;
    margin: 0;
  }

  #main-container{
    border: solid 1px #ccc;
    width: 600px;
    margin: 100px auto;
  }

  #header{
    background: black;
    padding: 10px;
  }

  h2{
    padding: 0 10px;
  }
</style>
