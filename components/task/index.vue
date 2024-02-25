<script setup lang="ts">
import { ref, watch, onMounted } from "vue";
import axios from "axios";

const emit = defineEmits();

const props = defineProps(["taskData"]);

const handleDone = async (id) => {
  try {
    const response = await axios.put(`http://localhost:3001/todos/${id}`, {
      completed: true,
      destination: props.taskData?.destination,
    });

    if (response) {
      emit("taskCompleted", id);
    }
    console.log(response);
  } catch (error) {
    console.log(error);
  }
};

const handleDelete = async (id) => {
  try {
    const response = await axios.delete(`http://localhost:3001/todos/${id}`);
    if (response) {
      // Emit an event to notify the parent component to refresh the task list
      emit("taskDeleted", id);
    }
  } catch (error) {
    console.log(error);
  }
};
</script>

<template>
  <div
    class="h-10 flex justify-between items-center border-2 p-3 bg-gray-300 mt-1 w-[350px]"
  >
    <h2 :class="{ 'line-through': taskData?.completed }">
      {{ taskData?.destination }}
    </h2>
    <div class="mr-2 flex gap-1">
      <button
        class="w-12 h-6 border-solid border-1 bg-green-500 rounded-sm"
        type="submit"
        @click="handleDone(taskData?.id)"
      >
        Done
      </button>
      <button
        class="w-14 h-6 border-solid border-1 bg-red-700 text-white rounded-sm"
        type="submit"
        @click="handleDelete(taskData?.id)"
      >
        Delete
      </button>
    </div>
  </div>
</template>
