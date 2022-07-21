<template>
  <!-- navbar -->
<TodoNavbarComponent />
    <!--Todo form -->
<TodoFormComponent />
</template>

<script>
import TodoNavbarComponent from './components/TodoComponents/TodoNavbarComponent.vue';
import TodoFormComponent from './components/TodoComponents/TodoFormComponent.vue'

export default {
    components: { TodoNavbarComponent , TodoFormComponent},
      
};
</script>
