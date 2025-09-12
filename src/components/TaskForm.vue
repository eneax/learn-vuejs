<script lang="ts" setup>
import { ref } from 'vue'

const newTask = ref('')

function formSubmit() {
  console.log('Form submitted', newTask.value)
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
