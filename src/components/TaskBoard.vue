<template>
  <div class="board">
    <h2>{{ title }}</h2>
    <div v-if="tasks.length === 0" class="empty">Vacío</div>
    <div 
      v-for="task in tasks" 
      :key="task.id" 
      class="task"
      @click="$emit('move', task)"
    >
      {{ task.name }}
    </div>
  </div>
</template>

<script setup>
defineProps({
  title: String,
  tasks: Array
})
</script>

<style scoped>
.board {
  width: 30%;
  background: #f2f2f2;
  padding: 10px;
  border-radius: 10px;
}

.task {
  background-color: #fff;
  border: 1px solid #ccc;
  padding: 8px;
  margin-bottom: 8px;
  border-radius: 5px;
  cursor: pointer;
  transition: transform 0.2s;
}

.task:hover {
  transform: scale(1.05);
  background-color: #e6ffe6;
}

.empty {
  color: gray;
  font-style: italic;
}
</style>
