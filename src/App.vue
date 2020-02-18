<template>
  <div id="app">
    <Header />
    <AddTodo v-on:addTodo="addTodo" />
    <Todos v-bind:todos="todos" v-on:delete="deleteTodo" />
  </div>
</template>

<script>
import Todos from "./components/Todos";
import Header from "./components/Layout/Header";
import AddTodo from "./components/AddTodo";
import axios from "axios";

export default {
  name: "App",
  components: { Todos, Header, AddTodo },
  methods: {
    deleteTodo(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(() => (this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => console.error(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;
      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => (this.todos = [...this.todos, res.data]))
        .catch(err => console.error(err));
    }
  },
  data() {
    return {
      todos: []
    };
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => (this.todos = res.data))
      .catch(err => console.error(err));
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  text-align: center;
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Oxygen,
    Ubuntu, Cantarell, "Open Sans", "Helvetica Neue", sans-serif;
}
</style>
