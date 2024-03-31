<template>
  <NuxtLayout>
    <div>
      <form @submit.prevent="addTask">
        <input placeholder="TODOを追加" v-model="newTask" name="newTask" autocomplete="off" />
        <button>追加</button>
      </form>
      <ul>
        <li v-for="(task, index) in tasks" :key="index">
          <span>{{ task }}</span>
          <button @click="deleteTask(index)">削除</button>
        </li>
      </ul>
      <button class="clearButton" @click="clearTasks">クリア</button>
    </div>
  </NuxtLayout>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { useTasksStore } from '@/stores/tasks'

const store = useTasksStore()
const newTask = ref('')

function addTask() {
  store.addTask(newTask.value)
  newTask.value = ''
}

function deleteTask(index: number) {
  store.deleteTask(index)
}

function clearTasks() {
  store.clearTasks()
}

const tasks = store.tasks
</script>