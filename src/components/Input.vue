<template>
  <div>
    <form @submit.prevent="onSubmit">
      <input
        type="text"
        class="todo-input"
        v-model="todotext"
        placeholder="Neue Aufgabe"
      />
      <button class="todo-button" type="submit">
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
  props: ["todo", "todos", "newTodo", "todotext"],
  methods: {
    onSubmit() {
      localStorage.setItem("todo", JSON.stringify(this.todotext));
      this.todotext.push(this.todotext);
      this.todotext = "";
    },
  },
};
</script>
