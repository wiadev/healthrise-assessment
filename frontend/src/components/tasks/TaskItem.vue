<template>
  <li>
    <h2>{{ task.title }}</h2>
    <editor-content :editor="editor" />
    <button @click="markDone">Complete</button>
  </li>
</template>

<script setup lang="ts">
  import { useEditor, EditorContent } from '@tiptap/vue-3'
  import StarterKit from '@tiptap/starter-kit'

  const props = defineProps(['task']);

  const editor = useEditor({
    content: props.task.description,
    extensions: [StarterKit],
  })

  function markDone() {
    // TO DO
  }
</script>

<!-- <script>
export default {
  name: 'TaskItem',
  props: ['task', 'setTasks', 'reload'],
  methods: {
    async markDone() {
      if (typeof this.task.status === 'string') this.task.status = 'Done';
      else this.task.status = 1;
      try {
        await this.reload();
      } catch (e) { }

    }
  }
};
</script> -->
