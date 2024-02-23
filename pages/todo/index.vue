<template>
  <div class="w-96 h-96 mt-12 items-center rounded-lg bg-white flex flex-col">
    <h1 class="text-3xl text-center mt-3 font-bold">Task board</h1>
    <h5 class="text-sm">Create a list tasks</h5>

    <div class="mt-8 flex gap-1">
      <input
        type="text"
        placeholder="Add a new task"
        class="w-60 h-10 focus:outline-none bg-gray-50 border border-gray-300 text-sm rounded-sm p-2"
      />
      <button
        type="submit"
        class="w-20 h-10 bg-green-500 rounded-sm text-white"
      >
        Add
      </button>
    </div>

    <!-- To do list -->
    <div class="border-solid border-2 border-sky-500 mt-4 w-80 h-52">
      <h1 class="text-center">List of task</h1>
      <Task />
      <Task />
      <Task />
      <Task />
    </div>
  </div>
</template>
