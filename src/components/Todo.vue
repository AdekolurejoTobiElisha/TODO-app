<template>
  <div>
    <div v-if="!editMode">
      <span @click="toggleEdit">{{ todo.title }}</span>
      <button @click="deleteTodo">Delete</button>
    </div>
    <div v-else>
      <input v-model="editedTodo" @keyup.enter="saveEdit" />
      <button @click="saveEdit">Save edit</button>
      <button @click="cancelEdit">Cancel edit</button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      editMode: false,
      editedTodo: this.todo.title,
    };
  },
  methods: {
    toggleEdit() {
      this.editMode = true;
    },
    saveEdit() {
      this.$emit("edit", { id: this.todo.id, title: this.editedTodo });
      this.editMode = false;
    },
    cancelEdit() {
      this.editMode = false;
      this.editedTodo = this.todo.title;
    },
    deleteTodo() {
      this.$emit("delete", this.todo.id);
    },
  },
};
</script>
