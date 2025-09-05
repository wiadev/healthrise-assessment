<template>
  <div>
    <ul>
      <!-- <TaskItem
        v-for="task in tasks"
        :task="task"
        :setTasks="setTasks"
        :reload="reload"
      /> -->
      <TaskItem v-for="task in tasks" :key="task.id" :task="task" />
    </ul>
  </div>
</template>

<script setup lang="ts">
import TaskItem from './TaskItem.vue';
defineProps(['tasks']);
</script>
<!-- <script>
import TaskItem from './TaskItem.vue';

export default {
  name: 'TaskList',
  props: ['tasks', 'setTasks', 'reload'],
  components: { TaskItem }
};
</script> -->
