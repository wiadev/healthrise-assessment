<template>
  <form @submit.prevent="submitTask">
    <div class="space-y-2">
      <div class="col-span-full">
        <label for="title" class="block text-sm/6 font-medium text-gray-900">Title</label>
        <div class="mt-2">
          <input v-model="title" id="title" class="block w-full rounded-md bg-white px-3 py-1.5 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 placeholder:text-gray-400 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6" />
        </div>
      </div>
      <div class="col-span-full">
        <label class="block text-sm/6 font-medium text-gray-900">Description</label>
        <custom-editor v-model="description" />
      </div>
      <div class="col-span-full">
        <label for="assignee" class="block text-sm/6 font-medium text-gray-900">Assign to </label>
        <div class="mt-2 grid grid-cols-1">
          <select id="assignee" v-model="assigneeId" class="col-start-1 row-start-1 w-full appearance-none rounded-md bg-white py-1.5 pr-8 pl-3 text-base text-gray-900 outline-1 -outline-offset-1 outline-gray-300 focus:outline-2 focus:-outline-offset-2 focus:outline-indigo-600 sm:text-sm/6">
            <option>User A</option>
            <option>User B</option>
            <option>User C</option>
          </select>
          <font-awesome-icon icon="fa-solid fa-chevron-down" class="pointer-events-none col-start-1 row-start-1 mr-2 size-5 self-center justify-self-end text-gray-500 sm:size-4" aria-hidden="true" />
        </div>
      </div>
      <div class="col-span-full">
        <label class="block text-sm/6 font-medium text-gray-900">Due date</label>
        <VueDatePicker v-model="dueDate" :format="format"></VueDatePicker>
      </div>
      <div class="col-span-full">
        <button type="submit" class="rounded-md bg-indigo-600 px-3 py-2 text-sm font-semibold text-white shadow-xs hover:bg-indigo-500 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-indigo-600">Create Task</button>
      </div>
    </div>
  </form>
</template>

<script setup lang="ts">
  import { ref } from 'vue'
  import CustomEditor from '@/components/CustomEditor.vue'
  import VueDatePicker from '@vuepic/vue-datepicker'
  import '@vuepic/vue-datepicker/dist/main.css'
  import { library } from '@fortawesome/fontawesome-svg-core'
  import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome'
  import { faChevronDown } from '@fortawesome/free-solid-svg-icons'

  library.add(faChevronDown)

  const title = ref('')
  const description = ref('')
  const assigneeId = ref('')
  const dueDate = ref('')

  const emit = defineEmits(['submit'])

  const format = (date: Date) => {
    const day = date.getDate();
    const month = date.getMonth() + 1;
    const year = date.getFullYear();

    return `${month}/${day}/${year}`;
  }

  function submitTask() {
    emit('submit', {
      title: title.value,
      description: description,
      assigneeId: title.value,
      dueDate: dueDate.value,
    })
  }
</script>
