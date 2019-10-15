<template>
  <div id="app">
    <h1>Todo App</h1>
    <add-todo @add-todo="addTodo"></add-todo>
    <div class="todos">
      <todo v-for="item in tasks" :key="item.id" :task="item" @delete-todo="deleteTodo"></todo>
    </div>
  </div>
</template>

<script>
import Todo from "./components/Todo";
import AddTodo from "./components/AddTodo";

export default {
  name: "App",
  data() {
    return {
      tasks: []
    };
  },
  components: {
    Todo,
    AddTodo
  },
  methods: {
    addTodo(task) {
      this.tasks.push(task);
    },
    deleteTodo(task) {
      this.tasks = this.tasks.filter(t => t.id !== task.id);
    }
  }
};
</script>

<style>
* {
  box-sizing: border-box;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  padding: 1.5rem;
}

.todos {
  width: 100%;
}

input {
  width: 80%;
  margin: 0.25rem;
  padding: 0.75rem 0.25rem;
  border: 2px solid grey;
  border-radius: 5px;
  transition: border-color 0.2s ease;
}

input:focus {
  border-color: #2ecc71;
}

button {
  color: white;
  background-color: #2ecc71;
  border: none;
  margin: 0.25rem;
  padding: 0.75rem;
  font-weight: 700;
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
}
</style>
