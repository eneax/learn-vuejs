<script lang="ts" setup>
import type { Task } from '../types';

const props = defineProps<{
  tasks: Task[]
}>()

const emits = defineEmits<{
  toggleDone: [id: string]
}>()
</script>

<template>
  <div class="task-list">
    <article v-for="task in props.tasks" :key="task.id">
      <label>
        <input type="checkbox" @input="emits('toggleDone', task.id)" :checked="task.completed" />
        <span :class="{ completed: task.completed }">{{ task.title }}</span>
      </label>
    </article>
  </div>
</template>

<style scoped>
.task-list {
  margin-top: 1rem;
}

.completed {
  text-decoration: line-through;
}
</style>