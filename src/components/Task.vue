<script setup>
import Status from './icons/IconTodo.vue'
import Priority from './icons/IconPriority.vue';
import Taskname from './icons/IconTaskLabel.vue';
import Delete from './icons/IconDeleteTask.vue';

import { ref } from 'vue'
import { Input } from 'postcss';
const emit = defineEmits(['priority-updated','status-updated','label-updated','delete-task']);

const { task } = defineProps(['task']);


const priorityList = ref(['Urgent','Important','Normal']);
const statusList = ref(['pending','inprogress','done']);
const priority = ref('');
const status = ref('');
const label = ref('');

if (task) {
  priority.value = task.priority || ''; // Assuming task.priority is a string
  status.value = task.status || ''; // Assuming task.status is a string
  label.value = task.label || ''; // Assuming task.label is a string
}

// to toggle the values of the priority 
function togglePriority() {
  const currentIndex = priorityList.value.indexOf(priority.value);
  const newIndex = (currentIndex + 1) % priorityList.value.length;
  priority.value = priorityList.value[newIndex];
  const taskid = task.id;
  emit('priority-updated', { id : taskid, priority: priority.value });

}

// to toggle the values of the priority 
function toggleStatus() {
  const currentIndex = statusList.value.indexOf(status.value);
  const newIndex = (currentIndex + 1) % statusList.value.length;
  status.value = statusList.value[newIndex];
  const taskid = task.id;
  emit('status-updated', { id : taskid, status: status.value });

}

// to update label value 
function updateLabelValue(newlabel){
  label.value = newlabel;
  const taskid = task.id;
  emit('label-updated', { id : taskid, newlabel });
  console.log('Updated Label:', newlabel);
}


// to delete task  
function delete_task(){
  emit('delete-task', { taskid:task.id });
}

</script>

<template>
  <div class="flex justify-between bg-slate-50 rounded-2xl text-gray-600 px-3 py-1 my-1 w-auto">  
    <Priority :priorityValue="priority" @togglePriority="togglePriority()" />
    <div class="flex justify-between px-3">
      <Status :statusValue="status" @toggleStatus="toggleStatus()"/> 
      <Taskname :labelStatusValue="status" :labelValue="label" @updateLabel="updateLabelValue($event)"/>
    </div>
    <Delete @deletetask="delete_task" />
    </div>
</template>
