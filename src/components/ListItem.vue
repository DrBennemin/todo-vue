<template>
  <div class="todo-container">
    <ul class="todo-list">
      <div class="todo" v-for="(todo, key) in tasks" :key="key">
        <li :class="{ completed: checkCompleted(todo) }" class="todo-item">
          {{ todo[0] }}
        </li>
        <button
          @click="completeTask(key), setClassCompleted(todo)"
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
      isCompleted: false,
    };
  },
  mounted() {
    // console.log(this.todos);
  },

  methods: {
    removeItem(key) {
      this.$emit("removeItemFromList", key);
    },
    completeTask(key) {
      this.$emit("setCompleteTask", key);
    },
    setClassCompleted(todo) {
      this.checkCompleted(todo);
    },
    checkCompleted(todo) {
      if (todo[1] == "completed") {
        return true;
      } else {
        return false;
      }
    },
  },
  computed: {
    completedTasks() {
      return this.todos.filter((todo) => todo[1] == "completed");
    },
    uncompletedTasks() {
      return this.todos.filter((todo) => todo[1] == "uncompleted");
    },
    tasks() {
      if (this.filter == "completed") {
        return this.completedTasks;
      } else if (this.filter == "uncompleted") {
        return this.uncompletedTasks;
      } else {
        return this.todos;
      }
    },
  },
};
</script>

<style></style>
