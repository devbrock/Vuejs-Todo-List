<template>
  <div>
    <h3>Todos</h3>
    <div v-for="todo in todos" v-bind:key="todo.id">
      <TodoItem v-bind:todo="todo" v-on:delete="$emit('delete', todo.id)" />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";

export default {
  name: "Todos",
  props: ["todos"],
  components: {
    TodoItem
  }
};
</script>

<style scoped>
</style>