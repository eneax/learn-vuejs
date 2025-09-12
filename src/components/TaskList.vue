<script lang="ts" setup>
import type { Task } from '../types';

const props = defineProps<{
  tasks: Task[]
}>()

const emits = defineEmits<{
  toggleDone: [id: string]
  deleteTask: [id: string]
}>()
</script>

<template>
  <div class="task-list">
    <article v-for="task in props.tasks" :key="task.id" class="task">
      <label>
        <input type="checkbox" @input="emits('toggleDone', task.id)" :checked="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
      </label>
      <Button class="outline" @click="emits('deleteTask', task.id)">Delete</Button>
    </article>
  </div>
</template>

<style>
.task-list {
  margin-top: 1rem;
}

.task {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.completed {
  text-decoration: line-through;
}
</style>