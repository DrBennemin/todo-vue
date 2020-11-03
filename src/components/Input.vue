<template>
  <div>
    <form>
      <input type="text" class="todo-input" />
      <button class="todo-button" @click="addNewTodo(todo)">
        <i class="fas fa-plus-square"></i>
      </button>
      <div class="select">
        <select name="todos" class="filter-todo">
          <option value="all">All</option>
          <option value="completed">Completed</option>
          <option value="uncompleted">Uncompleted</option>
        </select>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    addNewTodo: function() {
      //   this.todos.push(todo);
    },
  },
};
</script>
