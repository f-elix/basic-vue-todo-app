<template>
  <div class="todo">
    <p>{{ task.userInput }}</p>
    <button>Edit</button>
    <button @click="deleteTodo">Delete</button>
    <button>Mark as done</button>
  </div>
</template>

<script>
export default {
  props: ["task"],
  methods: {
    deleteTodo() {
      this.$emit("delete-todo", this.task.id);
    }
  }
};
</script>

<style scoped>
.todo {
  width: 100%;
  padding: 0.25rem;
  margin: 0.75rem auto;
  display: flex;
  border: 3px solid grey;
  border-radius: 5px;
}

.todo p {
  margin-right: auto;
  max-width: 50%;
  text-align: left;
}

.todo button {
  align-self: flex-start;
  margin: 0.75rem 0.25rem;
}
</style>
