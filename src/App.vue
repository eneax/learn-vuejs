<script lang="ts" setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue';

const title = ref('Tasks')

function addTask(newTask: string) {
  console.log('New Task:', newTask)
}
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm @add-task="addTask" />
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