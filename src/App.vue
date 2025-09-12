<script lang="ts" setup>
import { ref } from 'vue'
import TaskForm from './components/TaskForm.vue';

const title = ref('Tasks')
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <TaskForm />
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