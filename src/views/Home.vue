<template>
  <div id="app">
    <AddToDo v-on:add-todo="addTodo"/>
    <!-- equal sign 'todos' comes from array of objects -->
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo"/>
  </div>
</template>

<script>

import Todos from '../components/Todos';
import AddToDo  from '../components/AddTodo';
import axios from 'axios';

export default {
  name: 'Home',
  components: {
    Todos,
    AddToDo
    
  },
  data(){
    return{
      // todos is an array of objects
      todos:[]
    }
  },
  methods:{
    deleteTodo(id){
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(() => this.todos = this.todos.filter(todo => todo.id !== id))
      //? replace res => with () => which is actually empty parenthisis
      // .catch((error) => {console.log(error)})

      // return everything other than the id we've passed in 
      // this.todos = this.todos.filter(todo => todo.id !== id);
    },
    addTodo(newTodo){
      const {title, completed } = newTodo; // destructuring. get title and completed from newTodo obj
      axios.post("https://jsonplaceholder.typicode.com/todos",{title, completed}) // send title and completed to post
      .then(res => this.todos = [...this.todos, res.data])
      // .catch(err => console.log(err));
      // use spread operator(...) to copy whatever is in this.todos and add newTodo
      // this.todos = [...this.todos, newTodo];
    }

    },
  created(){
    // returns a promise
    axios.get("https://jsonplaceholder.typicode.com/todos?_limit=10")
    // set the new todos to be equal to res.data(i.e what is in the url provided)
    .then(res => this.todos = res.data)
    // .catch(err => console.log(err));
  },

}
</script>

<style>
/* reset style */
*{
  box-sizing: border-box;
  margin:0;
  padding:0;
}

body{
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
}

.btn{
  display:inline-block;
  border:none;
  background: #555;
  color: #fff;
  padding: 7px 20px;
  cursor: pointer;
}

.btn:hover{
  background: #666;
}
</style>
