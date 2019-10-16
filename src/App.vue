<template>
  <div id="app" :class="{ darkmode: isDarkmode }">
    <div class="options">
      <button @click="isDarkmode = !isDarkmode">
        {{ isDarkmode ? "Light Mode" : "Dark Mode" }}
      </button>
      <button @click="clearTodos">Clear list</button>
    </div>
    <h1>Todo List</h1>
    <add-todo-form @add-todo="addTodo"></add-todo-form>
    <div class="todos">
      <transition-group name="todo">
        <todo
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @delete-todo="deleteTodo"
          @edit-todo="saveTodos"
          @change-task-state="saveTodos"
        ></todo>
      </transition-group>
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";
import AddTodoForm from "./components/AddTodoForm";

export default {
  name: "App",
  data() {
    return {
      todos: [],
      isDarkmode: true
    };
  },
  components: {
    Todo,
    AddTodoForm
  },
  mounted() {
    if (localStorage.getItem("todos")) {
      this.todos = JSON.parse(localStorage.getItem("todos"));
    }
  },
  methods: {
    addTodo(todo) {
      const newTodo = {
        task: todo.task,
        id: todo.id,
        done: todo.done
      };
      this.todos.push(newTodo);
      this.saveTodos();
    },
    deleteTodo(id) {
      this.todos = this.todos.filter(t => t.id !== id);
      this.saveTodos();
    },
    saveTodos() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    clearTodos() {
      this.todos = [];
      this.saveTodos();
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  font-family: "Roboto", sans-serif;
  line-height: 1.5;
}

html {
  font-size: 14px;
}

body {
  padding: 0;
  margin: 0;
}

#app {
  min-height: 100vh;
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 1.5rem;
  position: relative;
  transition: color 0.4s ease, background-color 0.4s ease;
}

.darkmode {
  background-color: #222222;
  color: #fff;
}

.todos {
  width: 100%;
}

input,
textarea {
  width: 80%;
  margin: 0 0.25rem;
  padding: 0.5rem;
  border: 2px solid grey;
  border-radius: 5px;
  font-size: 1.5rem;
  transition: border-color 0.2s ease;
}

input:focus,
textarea:focus {
  border-color: #2ecc71;
}

button {
  color: white;
  background-color: #2ecc71;
  border: none;
  margin: 0.75rem 0.25rem;
  padding: 0.5rem 0.75rem;
  font-size: 1.5rem;
  border-radius: 5px;
  box-shadow: 1px 1px 3px black;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

button:hover {
  background-color: #1abc9c;
}

button:active {
  box-shadow: inset 1px 1px 3px black;
  outline: none;
}

.options {
  position: absolute;
  right: 10%;
  top: 0%;
}

.options button {
  font-size: 0.75rem;
}

/* Vue transitions */

.todo-enter,
.todo-leave-to {
  opacity: 0;
  transform: translateX(-150%);
}

.todo-enter-active {
  --transition-time: 0.4s;
  transition: opacity var(--transition-time),
    transform var(--transition-time) cubic-bezier(0.55, 0.57, 0.34, 1.34);
}

.todo-leave-active {
  --transition-time: 0.4s;
  transition: opacity var(--transition-time),
    transform var(--transition-time) cubic-bezier(0.67, -0.35, 0.27, 0.98);
}

@media screen and (min-width: 768px) {
  html {
    font-size: 16px;
  }
}
</style>
