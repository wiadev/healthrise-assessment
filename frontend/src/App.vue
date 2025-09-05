<template>
  <div class="flex">
    <div class="flex-1 p-2"><TaskForm @submit="addTask" /></div>
    <div class="flex-1 p-2"><TaskList :tasks="tasks" /></div>
  </div>
</template>

<script setup lang="ts">
import TaskForm from '@/components/tasks/TaskForm.vue';
import TaskList from '@/components/tasks/TaskList.vue';
import { type Task } from '@/types/Task';
import { ref } from 'vue';

const tasks = ref<Task[]>([]);

function addTask(task: { title: string; assigneeId: string; dueDate:string; }) {
  tasks.value.push({ id: tasks.value.length, ...task, status: 'to-do' });
}
</script>
