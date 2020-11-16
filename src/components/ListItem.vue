<template>
  <div class="todo" :class="{'completed': task.completed}">
    <div>{{ task.task }}></div> 
    <button @click="toggleTaskState(id)" class="completed-btn">
      <i class="fas fa-check"></i>
    </button>
    <button @click="deleteTaskItem(id)" class="delete-btn">
      <i class="fas fa-trash"></i>
    </button>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
    };
  },
  props: ["task", "id"],
  methods: {
    toggleTaskState: function(id) {
      let todosLocalStorage = JSON.parse(localStorage.getItem("todos"));
      todosLocalStorage[id].completed = !todosLocalStorage[id].completed;
      localStorage.setItem("todos", JSON.stringify(todosLocalStorage));  
      this.reloadTasks()
    },
    deleteTaskItem(id) {
      let todosLocalStorage = JSON.parse(localStorage.getItem("todos"));
      todosLocalStorage.splice(id, 1);
      localStorage.setItem("todos", JSON.stringify(todosLocalStorage));
      this.reloadTasks()
    },
    reloadTasks() {
      this.$emit('reload')
    }
  },
};
</script>
