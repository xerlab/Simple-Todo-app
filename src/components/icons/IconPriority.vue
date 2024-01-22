
<script setup>
  import IconComponent from './_IconTemplate.vue';
  const props = defineProps(['priorityValue']);

  // To change Icon color based on value of the priority came from prop
  const getIconColor = () => {
    switch (props.priorityValue){
      case 'Urgent':
        return 'text-red-500';
      case 'Important':
        return 'text-blue-400';
      case 'Normal':
        return 'text-green-500';
      default :
        return 'text-gray-300';
    };
  };


</script>

<template>
  <!-- Use the IconComponent and pass the specific icon name as a prop -->
  <IconComponent iconName="akar-icons:pointer-right-fill" @click="$emit('togglePriority')" :class="getIconColor()" />
</template>

