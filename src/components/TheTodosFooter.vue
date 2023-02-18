<template>
  <div>
    <p v-if="itemsLeft > 0">{{ itemsLeft }} items left</p>
    <select v-model="filterType" @change="handleChangeFilterType">
      <option value="all">All</option>
      <option value="active">Active</option>
      <option value="completed">Completed</option>
    </select>
    <button @click="handleClearCompleted">Clear completed</button>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue';

const props = defineProps({
  todos: {
    type: Array,
    required: true,
  },
});
const emit = defineEmits(['changeFilter', 'clearCompleted']);
const filterType = ref('all');

const itemsLeft = computed(() => {
  return props.todos.filter((todo) => todo.completed !== true).length;
});
const handleChangeFilterType = () => {
  emit('changeFilter', filterType.value);
};
const handleClearCompleted = () => {
  emit('clearCompleted');
};
</script>

<style scoped>
div {
  display: flex;
  gap: 10px;
}
</style>
