<script lang="ts" setup>
import { computed, ref } from 'vue'
import type { Task } from './types';

import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';

const title = ref('Tasks')
const tasks = ref<Task[]>([])

const totalTasksCompleted = computed(() => tasks.value.reduce((total, task) => task.completed ? total + 1 : total, 0))

function addTask(newTask: string) {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false
  })
}

function toggleDone(id: string) {
  const task = tasks.value.find(task => task.id === id)
  if (task) {
    task.completed = !task.completed
  }
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
    <h3 v-if="!tasks.length">Add a task to get started.</h3>
    <h3 v-else>{{ totalTasksCompleted }} / {{ tasks.length }} tasks completed</h3>
    <TaskList :tasks @toggle-done="toggleDone" />
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