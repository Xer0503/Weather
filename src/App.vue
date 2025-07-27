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
    <button @click="selectedView = 1" class="px-2 py-2 bg-blue-400 space-x-5 rounded-2xl active:bg-blue-700" >1</button>
    <button @click="selectedView = 2" class="px-2 py-2 bg-blue-400 space-x-5 rounded-2xl active:bg-blue-700" >2</button>
    <button @click="selectedView = 3" class="px-2 py-2 bg-blue-400 space-x-5 rounded-2xl active:bg-blue-700" >3</button>
    <component :is="views[selectedView]" />
  </div>
</template>

<style scoped>
</style>
