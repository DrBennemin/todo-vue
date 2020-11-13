<template>
  <div class="todo-container">
    <ul class="todo-list">
      <div class="todo" v-for="(todo, key) in filterTodos" :key="key">
        <!-- <li :class="{ completed: isCompleted }" class="todo-item"> -->
        <li :class="[isCompleted ? completed : ``]" class="todo-item">
          {{ todo.completed }}
          {{ todo.task || todo[0].task }}
        </li>
        <button
          @click="completeTask(key), toggleClassCompleted()"
          class="completed-btn"
        >
          <i class="fas fa-check"></i>
        </button>
        <button @click="removeItem(key)" class="delete-btn">
          <i class="fas fa-trash"></i>
        </button>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["todos", "filter"],
  data: function() {
    return {
      completed: `completed`,
      isCompleted: false,
    };
  },

  methods: {
    removeItem(key) {
      this.$emit("removeItemFromList", key);
    },
    completeTask(key) {
      this.$emit("toggleCompleteTask", key);
    },
    toggleClassCompleted() {
      this.isCompleted = !this.isCompleted;
      // this.checkCompleted(todo);
    },
  },
  computed: {
    filterTodos() {
      var filteredTodos;
      switch (this.filter) {
        case "completed":
          filteredTodos = this.todos.filter((todo) => todo.completed == true);
          break;
        case "uncompleted":
          filteredTodos = this.todos.filter((todo) => todo.completed == false);
          break;
        default:
          filteredTodos = this.todos;
          break;
      }
      return filteredTodos;
    },

    // completedTasks() {
    //   return this.todos.filter((todo) => todo.completed == true);
    // },
    // uncompletedTasks() {
    //   return this.todos.filter((todo) => todo.completed == false);
    // },
    // tasks() {
    //   if (this.filter == "completed") {
    //     return this.todos.filter((todo) => todo.completed == true);
    //   } else if (this.filter == "uncompleted") {
    //     return this.todos.filter((todo) => todo.completed == false);
    //   } else {
    //     return this.todos;
    //   }
    // },
  },
};
</script>

<style></style>
