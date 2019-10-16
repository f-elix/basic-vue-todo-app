<template>
  <form>
    <input type="text" v-model="task.userInput">
    <button @click="addTodo">Add task</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      task: {
        userInput: "",
        id: ""
      }
    };
  },
  computed: {
    generateId() {
      return (
        "_" +
        Math.random()
          .toString(36)
          .substr(2, 9)
      );
    }
  },
  methods: {
    addTodo() {
      if (this.task.userInput.length > 0) {
        this.task.id = this.generateId;
        this.$emit("add-todo", this.task);
      }
    }
  }
};
</script>

