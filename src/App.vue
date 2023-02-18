<template>
  <div>
    <TheTodosForm
      @mark-all-completed="handleMarkAllCompleted"
      @add-todo="handleAddTodo"
    />
    <TheTodosList
      @toggle-todo="handleToggleTodo"
      @delete-todo="handleDeleteTodo"
      :todos="filteredTodos"
    />
    <TheTodosFooter
      :todos="todos"
      @clear-completed="handleClearCompleted"
      @change-filter="handleChangeFilterType"
    />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';
import TheTodosFooter from './components/TheTodosFooter.vue';
import TheTodosForm from './components/TheTodosForm.vue';
import TheTodosList from './components/TheTodosList.vue';

const todos = ref([]);
const filterType = ref('all');

const filteredTodos = computed(() => {
  if (filterType.value === 'active') {
    return todos.value.filter((todo) => todo.completed === false);
  }
  if (filterType.value === 'completed') {
    return todos.value.filter((todo) => todo.completed === true);
  }
  return todos.value;
});

const handleAddTodo = (todo) => {
  todo.id = todos.value.length;
  todos.value.push(todo);
};
const handleDeleteTodo = (id) => {
  const todoIdx = todos.value.findIndex((todo) => todo.id === id);
  todos.value.splice(todoIdx, 1);
};
const handleToggleTodo = (id) => {
  const todoIdx = todos.value.findIndex((todo) => todo.id === id);
  todos.value[todoIdx].completed = !todos.value[todoIdx].completed;
};
const handleChangeFilterType = (type) => {
  filterType.value = type;
};
const handleClearCompleted = () => {
  todos.value = todos.value.filter((todo) => todo.completed !== true);
};
const handleMarkAllCompleted = () => {
  todos.value.forEach((todo) => (todo.completed = true));
};
</script>

<style lang="scss" scoped></style>
