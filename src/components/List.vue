<template>
  <div class="todo-container">
    <ul class="todo-list">
      <div class="todo" v-for="(todo, key) in filterTodos" :key="key">
        <list-item :task="todo" :id="key" @reload="loadTasks"></list-item>
      </div>
    </ul>
  </div>
</template>

<script>
import ListItem from "./ListItem";

export default {
  data: function() {
    return {
        tasks: []
    };
  },
  props: [
      "filter"
  ],
  components: {
      ListItem
  },
  mounted() {
      this.loadTasks()
  },
  computed: {
    filterTodos() {
      var filteredTodos;
      switch (this.filter) {
        case "completed":
          filteredTodos = this.tasks.filter((todo) => todo.completed == true);
          break;
        case "uncompleted":
          filteredTodos = this.tasks.filter((todo) => todo.completed == false);
          break;
        default:
          filteredTodos = this.tasks;
          break;
      }
      return filteredTodos;
    },
  },
  methods: {
      loadTasks() {
        this.tasks = JSON.parse(localStorage.getItem("todos"))
      },
  }
};
</script>
