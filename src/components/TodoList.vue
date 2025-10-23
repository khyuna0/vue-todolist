<template>
  <ul class="todoList">
    <li v-for="todo in todos" :key="todo.id" class="todoItem">
      {{ todo.content }}
      <button class="delete" @click="$emit('deleteTodo', todo.id)">삭제</button>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["todos"],
};
</script>

<style>
.todo-list {
  list-style: none;
  padding: 0;
}
.todoItem {
  display: 10px;
  gap: 10px;
}
</style>
