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
  <TransitionGroup name="task-list" tag="div" class="task-list">
    <article v-for="task in props.tasks" :key="task.id" class="task">
      <label>
        <input type="checkbox" @input="emits('toggleDone', task.id)" :checked="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
      </label>
      <Button class="outline" @click="emits('deleteTask', task.id)">Delete</Button>
    </article>
  </TransitionGroup>
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

.task-list-enter-active,
.task-list-leave-active {
  transition: all 0.5s ease;
}

.task-list-enter-from,
.task-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>