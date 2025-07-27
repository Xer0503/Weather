<script setup>
  import { ref } from 'vue';
  import UserPage from './pages/UserPage.vue';
  import TodoPage from './pages/TodoPage.vue';
  import WeatherPage from './pages/WeatherPage.vue';

  const selectedView = ref(3);
  const views = {
      1 : UserPage,
      2 : TodoPage,
      3 : WeatherPage
    }

</script>

<template>
  <div>
    <component :is="views[selectedView]" />
  </div>
</template>

<style scoped>
</style>
