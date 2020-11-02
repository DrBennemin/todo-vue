<template>
  <div>
    <body>
      <header>
        <h1>Benne's & Alex's Todo List</h1>
      </header>
      <form>
        <input type="text" class="todo-input" />
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
      <div class="todo-container">
        <ul class="todo-list"></ul>
      </div>
    </body>
  </div>
</template>

<script>
export default {};
</script>
