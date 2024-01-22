<script setup>
  const props = defineProps(['labelStatusValue','labelValue']);

  // To change Icon color based on value of the priority came from prop
  const gettextdecoration = () => {
    switch (props.labelStatusValue){
      case 'done':
        return 'line-through text-gray-400 focus:outline-none focus:ring-1 ring:bg-slate-400 ';
      default :
        return 'no-underline focus:outline-none focus:ring-1 ring:bg-slate-400';
    };
  };


</script>

<template>
    <div class="flex items-center icons_spaces w-96 " >
      <p contenteditable="true" @blur=" $emit('updateLabel',$event.target.textContent) " :class="gettextdecoration()" >{{labelValue}}</p>
    </div>
  </template>
  