<template>
  <div>
    <button @click="handleMarkAllCompleted">Mark all completed</button>
    <form @submit.prevent="handleSubmit">
      <input v-model="todo" type="text" />
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
const emit = defineEmits(['addTodo', 'markAllCompleted']);
const todo = ref('');

const handleSubmit = () => {
  emit('addTodo', {
    title: todo.value,
    completed: false,
  });
  todo.value = '';
};
const handleMarkAllCompleted = () => {
  emit('markAllCompleted');
};
</script>

<style scoped>
div {
  display: flex;
}
</style>
