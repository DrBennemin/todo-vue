<template>
  <div id="app">
    <body>
      <Header />
      <Input
        v-on:addTodoFromInput="onAddTodo"
        :todos="todos"
        v-on:onChangeFilter="filterTodos"
      />
      <ListItem
        v-on:toggleCompleteTask="toggleCompleteTask"
        v-on:removeItemFromList="onRemoveItem"
        :todos="todos"
        :filter="activeFilter"
      />
    </body>
  </div>
</template>

<script>
import Header from "./components/Header";
import Input from "./components/Input";
import ListItem from "./components/ListItem";

export default {
  name: "App",
  components: {
    Header,
    Input,
    ListItem,
  },
  data: function() {
    return {
      todos: JSON.parse(localStorage.getItem("todos")),
      activeFilter: "all",
    };
  },
  computed: {
    completed: function() {
      let todos = JSON.parse(localStorage.getItem("todos"));
      todos.filter("completed");
      return todos;
    },
  },
  methods: {
    onAddTodo: function(todo) {
      if (this.todos == null) {
        this.todos = [todo];
      } else {
        this.todos.push(todo);
      }
    },
    onRemoveItem: function(key) {
      let todosLocalStorage = JSON.parse(localStorage.getItem("todos"));
      todosLocalStorage.splice(key, 1);
      localStorage.setItem("todos", JSON.stringify(todosLocalStorage));
      this.todos.splice(key, 1);
    },

    toggleCompleteTask: function(key) {
      let todosLocalStorage = JSON.parse(localStorage.getItem("todos"));
      // todosLocalStorage[key].splice(1, 1, true);
      // todosLocalStorage[key].completed = true;
      todosLocalStorage[key].completed = !todosLocalStorage[key].completed;
      localStorage.setItem("todos", JSON.stringify(todosLocalStorage));
    },

    filterTodos: function(filter) {
      this.activeFilter = filter;
    },
  },
};
</script>

<style>
#app {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  background-image: linear-gradient(120deg, #023e8a, #ffc2cc);
  color: white;
  font-family: "Poppins", sans-serif;
  min-height: 100vh;
}

header {
  font-size: 1.5rem;
}

header,
form {
  min-height: 20vh;
  display: flex;
  justify-content: center;
  align-items: center;
}

form input,
form button {
  padding: 0.5rem;
  font-size: 2rem;
  border: none;
  background: white;
  outline: none;
}

form button {
  color: #023e8a;
  background: white;
  cursor: pointer;
  transition: all 0.3s ease;
}

form button:hover {
  background-color: #023e8a;
  color: white;
}

.todo-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.todo-list {
  min-width: 30%;
  list-style: none;
}

.todo {
  margin: 0.5rem;
  background-color: white;
  color: black;
  font-size: 1.5rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  transition: all 0.5s ease;
}

.todo li {
  flex: 1;
  width: 90vw;
}

.delete-btn,
.completed-btn {
  background: #023e8a;
  color: white;
  border: none;
  padding: 1rem;
  cursor: pointer;
  font-size: 1rem;
  outline: none;
}

.completed-btn {
  background: green;
}

.todo-item {
  padding: 0 0.5rem;
}

.fa-trash,
.fa-check {
  pointer-events: none;
}

.completed {
  text-decoration: line-through;
  opacity: 0.5;
}

.fall {
  transform: translateY(8rem) rotateZ(20deg);
  opacity: 0;
}

select {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  outline: none;
  border: none;
  color: #023e8a;
  width: 10rem;
  cursor: pointer;
  padding: 1rem;
}

.select {
  margin: 1rem;
  position: relative;
  overflow: hidden;
}

.select::after {
  content: "\25bc";
  position: absolute;
  background: #023e8a;
  top: 0;
  right: 0;
  padding: 1rem;
  pointer-events: none;
}

.select:hover::after {
  background: white;
  color: #023e8a;
}
</style>
