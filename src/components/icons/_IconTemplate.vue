<script setup>
  import { Icon } from '@iconify/vue';

  // Define a prop for the icon name
  const props = defineProps(['iconName','iconcolor']);
</script>

<template>
  <div class="flex items-center pr-2" >
    <Icon :icon="iconName"/>
  </div>
</template>