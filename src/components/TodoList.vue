<template>
  <div>
    <div v-for="todo in todos" :key="todo.id">
      <Todo :todo="todo" @delete="deleteTodo" @edit="editTodo" />
    </div>
    <div>
      <input
        v-model="newTodo"
        @keyup.enter="addTodo"
        placeholder="Add a new todo"
      />
      <button @click="addTodo">Add</button>
    </div>
  </div>
</template>

<script>
import Todo from "./Todo.vue";

export default {
  components: {
    Todo,
  },
  data() {
    return {
      todos: [],
      newTodo: "",
      nextId: 1,
    };
  },
  methods: {
    addTodo() {
      if (this.newTodo.trim() === "") return;
      this.todos.push({ id: this.nextId++, title: this.newTodo });
      this.newTodo = "";
    },
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => todo.id !== id);
    },
    editTodo({ id, title }) {
      const index = this.todos.findIndex((todo) => todo.id === id);
      this.$set(this.todos, index, { id, title });
    },
  },
};
</script>
