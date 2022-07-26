<script>
let id = 0;
export default {
  mounted() {
    this.$refs.c.textContent = "Is mounted";
  },
  data() {
    return {
      todos: [],
      hideCompleted: false,
      newTodo: "",
    };
  },
  computed: {
    // updates when the dependencies change
    filteredTodos() {
      return this.hideCompleted
        ? this.todos.filter((todo) => !todo?.done)
        : this.todos;
    },
  },
  methods: {
    addTodo(e) {
      e.preventDefault();
      this.todos.push({ id: id++, text: this.newTodo, done: false });
      this.newTodo = "";
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    showOrHide() {
      this.hideCompleted = !this.hideCompleted;
    },
  },
};
</script>

<template>
  <h1>To do</h1>
  <br />
  <form @submit="addTodo">
    <input type="text" v-model="newTodo" />
    <input type="submit" value="Add" />
  </form>
  <ul>
    <li v-if="!todos">No todo's in the list</li>
    <li v-else v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />

      <span :class="{ done: todo.done }">{{ todo.text }}</span>

      <button @click="deleteTodo(todo.id)">X</button>
    </li>
    <button @click="showOrHide">
      {{ hideCompleted ? "Show All" : "Hide completed" }}
    </button>
  </ul>

  <p ref="c"></p>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
