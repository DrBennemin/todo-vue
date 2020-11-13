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
        <select
          v-model="option"
          name="todos"
          class="filter-todo"
          @change="onChangeFilter()"
        >
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
  props: ["todo", "todos"],
  data: function() {
    return {
      todotext: "",
      option: "all",
    };
  },
  methods: {
    onSubmit() {
      if (localStorage.getItem("todos") !== null) {
        let todosLocalStorage = JSON.parse(localStorage.getItem("todos"));
        todosLocalStorage.push({ task: this.todotext, completed: false });
        localStorage.setItem("todos", JSON.stringify(todosLocalStorage));
      } else {
        localStorage.setItem(
          "todos",
          JSON.stringify([{ task: this.todotext, completed: false }])
        );
      }
      this.$emit("addTodoFromInput", { task: this.todotext, completed: false });
      this.todotext = "";
    },

    displayItem(attribueValue, todo) {
      todo.style.display = attribueValue;
    },

    onChangeFilter() {
      this.$emit("onChangeFilter", this.option);
    },
  },
};
</script>
