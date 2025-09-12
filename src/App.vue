<script lang="ts" setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue';
import type { Task } from './types';

const title = ref('Tasks')
const tasks = ref<Task[]>([])

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false
  })
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
    <article v-for="task in tasks" :key="task.id">
      {{ task.title }}
    </article>
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 1rem auto;
}

.button-container {
  display: flex;
  justify-content: flex-end;
}
</style>