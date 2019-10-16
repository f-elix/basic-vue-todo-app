<template>
  <div class="todo">
    <div class="todo__text">
      <transition name="edit" mode="out-in">
        <textarea
          name="Task"
          cols="30"
          rows="1"
          v-model="todo.task"
          v-if="editing"
        ></textarea>
        <p v-else :class="{ done: todo.done }">{{ todo.task }}</p>
      </transition>
    </div>
    <div class="todo__buttons">
      <button @click="editTodo" :class="{ disabled: todo.done }">
        {{ editing ? "Save" : "Edit" }}
      </button>
      <button @click="deleteTodo">Delete</button>
      <button @click="markDone" :class="{ disabled: editing }">
        {{ todo.done ? "Not done" : "Done" }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: ["todo"],
  data() {
    return {
      editing: false,
      userInput: ""
    };
  },
  methods: {
    deleteTodo() {
      this.$emit("delete-todo", this.todo.id);
    },
    editTodo() {
      this.editing = !this.editing;
      this.$emit("edit-todo");
    },
    markDone() {
      this.todo.done = !this.todo.done;
      this.$emit("change-task-state");
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
  font-size: 1.5rem;
  display: flex;
  flex-wrap: wrap;
  overflow: hidden;
}

.todo__text {
  flex-basis: 100%;
  height: 4.5rem;
  display: flex;
  align-items: center;
}

.todo p {
  margin: 0.25rem;
  text-align: left;
}

.todo textarea {
  width: 100%;
  font-size: inherit;
}

.todo button {
  align-self: flex-start;
  margin: 0.75rem 0.25rem;
}

.done {
  text-decoration: line-through;
}

button.disabled {
  pointer-events: none;
  opacity: 0.3;
}

/* Vue transition */

.edit-enter,
.edit-leave-to {
  opacity: 0;
  transform: translateY(-6rem);
}

.edit-enter-active,
.edit-leave-active {
  transition: all 0.3s ease-out;
}

@media screen and (min-width: 768px) {
  .todo {
    max-width: 52.5rem;
    justify-content: space-between;
  }

  .todo__text {
    flex-basis: 60%;
  }

  .todo__buttons {
    flex-basis: 40%;
  }
}
</style>
