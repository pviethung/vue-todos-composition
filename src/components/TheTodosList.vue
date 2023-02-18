<template>
  <div>
    <ul>
      <li v-for="todo in todos" :key="todo.title">
        <input
          type="checkbox"
          @change="handleToggleStatus(todo.id)"
          :checked="todo.completed"
        />
        <p>{{ todo.title }}</p>
        <button @click="handleDelete(todo.id)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
});
const emit = defineEmits(['deleteTodo', 'toggleTodo']);

const handleDelete = (id) => {
  emit('deleteTodo', id);
};
const handleToggleStatus = (id) => {
  emit('toggleTodo', id);
};
</script>

<style scoped>
ul {
  list-style: none;
  padding: 0;
}
li {
  display: flex;
  gap: 10px;
}
</style>
