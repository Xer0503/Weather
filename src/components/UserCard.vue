<script setup>
const { user } = defineProps({
  user: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div class="p-4 bg-white rounded shadow">
    <h2 class="text-lg font-bold">{{ user.name }}</h2>
    <p class="text-sm text-gray-500">{{ user.email }}</p>
  </div>
</template>