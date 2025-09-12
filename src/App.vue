<script lang="ts" setup>
import { computed, ref } from 'vue'
import type { Task, TaskFilter } from './types';

import TaskForm from './components/TaskForm.vue';
import TaskList from './components/TaskList.vue';
import FilterButton from './components/FilterButton.vue';

const title = ref('Tasks')
const tasks = ref<Task[]>([])
const filter = ref<TaskFilter>("all")

const totalTasksCompleted = computed(() => tasks.value.reduce((total, task) => task.completed ? total + 1 : total, 0))

const filteredTasks = computed(() => {
  switch (filter.value) {
    case 'all':
      return tasks.value
    case 'completed':
      return tasks.value.filter(task => task.completed)
    case 'todo':
      return tasks.value.filter(task => !task.completed)
    default:
      return tasks.value
  }
})

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

function deleteTask(id: string) {
  const index = tasks.value.findIndex(task => task.id === id)
  if (index !== -1) {
    tasks.value.splice(index, 1)
  }
}

function setFilter(value: TaskFilter) {
  filter.value = value
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
    <h3 v-if="!tasks.length">Add a task to get started.</h3>
    <h3 v-else>{{ totalTasksCompleted }} / {{ tasks.length }} tasks completed</h3>
    <div v-if="tasks.length" class="button-container">
      <FilterButton filter="all" @set-filter="setFilter" :currentFilter="filter" />
      <FilterButton filter="todo" @set-filter="setFilter" :currentFilter="filter" />
      <FilterButton filter="completed" @set-filter="setFilter" :currentFilter="filter" />
    </div>
    <TaskList :tasks="filteredTasks" @toggle-done="toggleDone" @delete-task="deleteTask" />
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
  gap: 0.5rem;
}
</style>