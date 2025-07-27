<script setup>
import { ref, onMounted } from 'vue'
import api from '../services/api'
import UserCard from '../components/UserCard.vue'

const users = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await api.get('/users')
    users.value = response.data
  } catch (err) {
    error.value = 'Failed to fetch users.'
    console.error(err)
  } finally {
    loading.value = false
  }
})
</script>

<template>
  <section class="p-4">
    <h1 class="text-xl font-bold mb-4">User List</h1>

    <div v-if="loading">Loading...</div>
    <div v-else-if="error">{{ error }}</div>
    <div v-else class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-4">
      <UserCard v-for="user in users" :key="user.id" :user="user" />
    </div>
  </section>
</template>
