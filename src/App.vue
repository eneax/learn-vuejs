<script lang="ts" setup>
import { ref } from 'vue'

const title = ref('Tasks')
const newTask = ref('')
</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <form action="">
      <label>
        New Task
        <input name="newTask" v-model="newTask">
      </label>
      <div class="button-container">
        <button>Add</button>
      </div>
    </form>
  </main>
</template>

<style scoped>
main {
  max-width: 800px;
  margin: 1rem auto;
}

.button-container {
  display: flex;
  justify-content: flex-end;
}
</style>