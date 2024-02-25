<script setup lang="ts">
import axios from "axios";
import { ref } from "vue";
const task = ref("");
const dest = ref([]);

const getTask = async () => {
  try {
    const { data } = await axios.get("http://localhost:3001/todos");
    dest.value = data || [];
  } catch (error) {
    console.log(error);
  }
};

const handleTaskCompleted = (taskId) => {
  const taskIndex = dest.value.findIndex((task) => task.id === taskId);
  if (taskIndex !== -1) {
    dest.value[taskIndex].completed = true;
  }
};

const handleCreateTask = async () => {
  try {
    const response = await axios.post("http://localhost:3001/todos", {
      destination: task.value,
      completed: false,
    });

    if (response) {
      task.value = "";
      getTask();
    }
  } catch (error) {
    console.log(error);
  }
};

const handleTaskDeleted = (taskId) => {
  dest.value = dest.value.filter((task) => task.id !== taskId);
};
getTask();
</script>

<template>
  <div
    class="w-[600px] h-96 mt-12 items-center rounded-lg bg-white flex flex-col"
  >
    <h1 class="text-3xl text-center mt-3 font-bold">Task board</h1>
    <h5 class="text-sm">Create a list tasks</h5>

    <div class="mt-8 flex gap-1">
      <input
        type="text"
        placeholder="Add a new task"
        class="w-60 h-10 focus:outline-none bg-gray-50 border border-gray-300 text-sm rounded-sm p-2"
        v-model="task"
      />
      <button
        type="submit"
        class="w-20 h-10 bg-green-500 rounded-sm text-white"
        @click="handleCreateTask"
      >
        Add
      </button>
    </div>

    <!-- To do list -->
    <div
      class="border-solid border-2 border-sky-500 mt-4 w-96 h-52 overflow-y-auto"
    >
      <h1 class="text-center">List of task</h1>
      <!-- Use `dest` instead of `destination` for v-for loop -->
      <Task
        v-for="(task, index) in dest"
        :key="index"
        :taskData="task"
        @taskDeleted="handleTaskDeleted"
        @taskCompleted="handleTaskCompleted"
      />
    </div>
  </div>
</template>
