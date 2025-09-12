<script lang="ts" setup>
import { ref } from 'vue'

const emit = defineEmits<{
  addTask: [newTask: string]
}>()

const newTask = ref('')

function formSubmit() {
  if (newTask.value.trim()) {
    emit('addTask', newTask.value.trim())
    newTask.value = ''
  }
}
</script>

<template>
  <form @submit.prevent="formSubmit">
    <label>
      New Task
      <input name="newTask" v-model="newTask">
    </label>
    <div class="button-container">
      <button>Add</button>
    </div>
  </form>
</template>
