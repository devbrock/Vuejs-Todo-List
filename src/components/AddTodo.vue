<template>
  <div>
    <form v-on:submit="addTodo">
      <input type="text" v-model="title" name="title" placeholder="Add todo..." />
      <input type="submit" value="Add Todo" />
    </form>
  </div>
</template>

<script>
import uuid from "uuid";

export default {
  name: "AddTodo",
  methods: {
    addTodo(e) {
      e.preventDefault();
      const newTodo = {
        id: uuid(),
        title: this.title,
        completed: false
      };

      this.$emit("addTodo", newTodo);
      this.title = "";
    }
  },
  data() {
    return {
      title: ""
    };
  }
};
</script>

<style scoped></style>
