<template>
  <div class="home">
      <AddTodo v-on:addToDo="addToList" v-bind:currentID="this.todos[this.todos.length-1].id"/>
      <Todos v-on:box-clicked="deleteTodo" v-bind:todos="this.todos"/>
  </div>
</template>

<script>
import Todos from '../components/Todos'
import AddTodo from '../components/AddTodo'
export default {
  name: 'home',
  components: {
    Todos,
    AddTodo
  },
  data(){
    return {
      todos:''
    }
  },
  methods: {
    deleteTodo(param){
       fetch(`https://jsonplaceholder.typicode.com/todos/${param}`,{
         method:"DELETE"
       })
       this.todos = this.todos.filter(todo => todo.id !== param)
     
    },
    addToList(todo){
        const {title,completed,id} = todo
        console.log(title,id)
       fetch(`https://jsonplaceholder.typicode.com/todos/`,{
         method:"POST",
         body:JSON.stringify({
           id,
           title,
           completed
         }),
          headers: {
      "Content-type": "application/json; charset=UTF-8"
    }
       }).then(res => res.json()).then(data =>this.todos = [...this.todos,data])
    }
  },

  created() {
    fetch('https://jsonplaceholder.typicode.com/todos?_limit=5')
    .then(res => res.json())
    .then(data => this.todos = data)
  }
}
</script>
