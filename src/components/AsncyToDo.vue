<template>
  <h1>Asynchronous Todos from Api</h1>
  <br />
  <div>
    <button @click="fetchTodo">Fetch next todo</button>
    <h1 v-if="!asyncTodos">Loading...</h1>
    <h1 v-else>{{ asyncTodos }}</h1>
  </div>
</template>

<script>
export default {
  data() {
    return { asyncTodos: {}, todoId: 1 };
  },
  mounted() {
    this.fetchTodos();
  },
  methods: {
    async fetchTodos() {
      let res = await fetch(
        `https://jsonplaceholder.typicode.com/todos/${this.todoId}`
      );
      this.asyncTodos = await res.json();
    },
    fetchTodo() {
      this.todoId++;
    },
  },
  watch: {
    todoId() {
      this.fetchTodos();
    },
  },
};
</script>
