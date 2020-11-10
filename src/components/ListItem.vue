<template>
  <div class="todo-container">
    <ul class="todo-list">
      <div class="todo" v-for="(todo, key) in todos" :key="key">
        <li class="todo-item">
          {{ todo[0] }}
        </li>
        <button class="completed-btn">
          <i class="fas fa-check"></i>
        </button>
        <button class="delete-btn">
          <i class="fas fa-trash"></i>
        </button>
      </div>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["todos"],
  mounted() {
    console.log(this.todos);
  }
};
</script>

<style></style>
