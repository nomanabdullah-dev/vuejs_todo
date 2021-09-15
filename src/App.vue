<template>
  <div id="app">
    <div class="todoListContainer">
      <div class="heading">
        <h2 id="title">Todo List</h2>
        <add-todo-form
        v-on:todoChanged="getTodos()" />
      </div>
      <todo-view 
        :todos="todos"
        v-on:todoChanged="getTodos()" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import addTodoForm from './components/addTodoForm.vue'
import TodoView from './components/todoView.vue'
export default {
  components: { addTodoForm, TodoView },
  data() {
    return {
      todos: []
    }
  },
  methods: {
    getTodos(){
      axios.get('http://127.0.0.1:3333/todo')
      .then(response => {
        this.todos = response.data
      })
      .catch(error => {
        console.log(error)
      })
    }
  },
  created(){
    this.getTodos()
  }
}
</script>


<style>
.todoListContainer{
  width: 350px;
  margin: auto;
}
.heading{
  background: #e6e6e6;
  padding: 10px;
}
#title{
  text-align: center;
}
</style>
