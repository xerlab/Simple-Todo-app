<script setup>
import { onMounted } from 'vue';

import TaskComponent from './components/Task.vue'
import { ref,watch } from 'vue'

const filteredtasks = ref([]);
const filterType = ref('all');
const newTask = ref('');
const tasks = ref([]);

// generating unique id for the task
const generateUniqueId = () => {
  return Date.now().toString();
};

// Function to handle the priority update from the child component
function handlePriorityUpdate({ id, priority }) {
  const task = tasks.value.find(task => task.id === id);
  if (task) {
    // Update the priority in the tasks array if needed
    task.priority = priority;
    console.log('All tasks:', tasks.value);
  } else {
    console.warn(`Task with id ${id} not found.`);
  }
}

// Parent Component
function handleStatusUpdate({ id, status }) {
  const task = tasks.value.find(task => task.id === id);
  if (task) {
    task.status = status;
    console.log('All tasks:', tasks.value);
  } else {
    console.warn(`Task with id ${id} not found.`);
  }
}


// Function to handle the label update from the child component
function handleLabelUpdate({ id, newlabel }) {
  const task = tasks.value.find(task => task.id === id);

  if (task) {
    // Update the label in the tasks array if needed
    task.label = newlabel;
    console.log('All tasks:', tasks.value);
  } else {
    console.warn(`Task with id  not found.`);
  }
}


// Function to handle delete task
function handledeletetask({ taskid }) {
    console.log("Before delete",tasks.value)
    //tasks.value = tasks.value.filter(task => task.id !== taskid);
    const index = tasks.value.findIndex(task => task.id === taskid);
    if (index !== -1) {
      tasks.value.splice(index, 1);
      console.log(`Task deleted with id ${taskid}`);
    } else {
      console.error(`Task with id ${taskid} not found`);
    }
    console.log("After delete",tasks.value)
}


// Function to add new taask in the tasks 
const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push({
      priority: 'Normal',  // You can set the default priority as needed
      status: 'pending',
      label: newTask.value,
      id: generateUniqueId(),
    });

    // Clear the input after adding the task
    newTask.value = '';
  }
};

onMounted(() => {
  filtertasks('all'); // Initial load, show all tasks
});

// to update the filter value on click ( all, pending )
const filtertasks = (type) => {
  filterType.value = type;
};

// Watch for changes in the filterType
watch(() => filterType.value, () => {
  // Regenerate filtered tasks when filterType changes
  regenerateFilteredTasks();
});

// Separate function to regenerate filtered tasks
const regenerateFilteredTasks = () => {
  if (filterType.value === 'all') {
    filteredtasks.value = tasks.value;
  } else if (filterType.value === 'pending') {
    filteredtasks.value = tasks.value.filter(task => task.status !== 'done');
  }
  console.log("These are the pending tasks:", filteredtasks.value);
};

</script>

<template>
  <div class="flex flex-col w-fit bg-slate-500 p-4 rounded-3xl">
    <h3 class="py-2">The simple todo app</h3>
    <input 
      class="bg-slate-400 rounded-2xl py-1 px-3 mb-3 text-white placeholder:text-gray-300 focus:outline-none focus:drop-shadow-lg" 
      v-model="newTask" 
      @keydown.enter="addTask" 
      placeholder="Add new task" 
      @keyup.enter="addTask" > 
    <TaskComponent
      v-for="(task, index) in filteredtasks" :key="task.id" :task="{...task,id: task.id}"
      @priority-updated="handlePriorityUpdate"
      @status-updated="handleStatusUpdate"
      @label-updated="handleLabelUpdate"
      @delete-task="handledeletetask"
    />
    
    <br>
    <div class="flex flex-row gap-3"> 
      <button class="bg-slate-700 w-full px-3 py-1 rounded-xl text-sm hover:bg-slate-800" @click="filtertasks('pending')">Pending</button>
      <button class="bg-slate-700 w-full px-3 py-1 rounded-xl text-sm hover:bg-slate-800" @click="filtertasks('all')">All tasks</button>
    </div>
  </div>
</template>
