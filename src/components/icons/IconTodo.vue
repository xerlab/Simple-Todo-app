
<script setup>
  import IconComponent from './_IconTemplate.vue';

  const props = defineProps(['statusValue']);

  // To change Icon color based on value of the priority came from prop
  const getIconColor = () => {
    switch (props.statusValue){
      case 'pending':
        return 'text-gray-400';
      case 'inprogress':
        return 'text-green-500';
      case 'done':
        return 'text-blue-500';
      default :
        return 'text-gray-300';
    };
  };

</script>

<template>
  <!-- Use the IconComponent and pass the specific icon name as a prop -->
  <IconComponent iconName="akar-icons:circle-check" @click="$emit('toggleStatus')" :class="getIconColor()"/>
</template>


<!--

<script setup>
  import { ref } from 'vue';
  import { taskstore } from '../../stores/counter';
  import IconComponent from './_IconTemplate.vue';


  // the icon has two colors for two status
  // when you click the status changes
  // when you hover the color changes

  const status = ref('todo');
  const iconcolor = ref('#CCCCCC');
  
  // change the status on click ( todo : done )
  const togglestatus = () => {
    status.value = status.value === 'todo' ? 'done' : 'todo' ;
    taskstore.updateStatus(status.value);
    togglecolor();
  };

  // change the color based on current status 
  const togglecolor = () => {
    iconcolor.value = status.value === 'todo' ? '#CCCCCC' : '#2BB8E4' ;
  };

  // change the color on hover 
  const mouseovercolor = () => {
    iconcolor.value = '#2BB8E4';
  
  }

</script>

<template>
  <div class="flex items-center icons_spaces"  
    @click="togglestatus" 
    @mouseover="mouseovercolor"
    @mouseleave="togglecolor"
    >
    
     -- Use the IconComponent and pass the specific icon name as a prop --
    <IconComponent iconName="akar-icons:circle-check"  :color="iconcolor"/>
    </div>
</template>


-->