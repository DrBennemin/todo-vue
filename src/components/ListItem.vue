<template>
  <div class="todo-container">
    <ul class="todo-list">
      <li class="todo" v-for="(todo, key) in todos" :key="key">
        {{ todo }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["todos"],
};
</script>

<style></style>
