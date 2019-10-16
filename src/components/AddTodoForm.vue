<template>
  <form class="form">
    <input type="text" v-model="userInput" class="input" />
    <button @click.prevent="addTodo" class="add-btn">Add task</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      userInput: "",
      todo: {
        task: "",
        id: "",
        done: false
      }
    };
  },
  methods: {
    generateId() {
      return (
        "_" +
        Math.random()
          .toString(36)
          .substr(2, 9)
      );
    },
    addTodo() {
      if (this.userInput.length > 0) {
        this.todo.id = this.generateId();
        this.todo.task = this.userInput;
        this.$emit("add-todo", this.todo);
        this.userInput = "";
      }
    }
  }
};
</script>

<style scoped>
.form .input,
.form .add-btn {
  width: 100%;
}

@media screen and (min-width: 924px) {
  .form .input {
    max-width: 45rem;
  }
  .form .add-btn {
    width: auto;
  }
}
</style>
