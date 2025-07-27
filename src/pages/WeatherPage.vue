<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

// State
const lat = ref(null)
const lon = ref(null)
const weather = ref(null)
const loading = ref(true)
const errorMsg = ref('')

// Your WeatherAPI key
const apiKey = 'e6bf2b2b1c324f88acf31802252707'

onMounted(() => {
  if (navigator.geolocation) {
    navigator.geolocation.getCurrentPosition(
      async (position) => {
        lat.value = position.coords.latitude
        lon.value = position.coords.longitude
        await fetchWeather()
      },
      (error) => {
        loading.value = false
        errorMsg.value = 'Location permission denied or error occurred.'
        console.error(error)
      }
    )
  } else {
    loading.value = false
    errorMsg.value = 'Geolocation is not supported by this browser.'
  }
})

// Fetch weather data from WeatherAPI
async function fetchWeather() {
  try {
    const res = await axios.get('https://api.weatherapi.com/v1/current.json', {
      params: {
        key: apiKey,
        q: `${lat.value},${lon.value}`
      }
    })
    weather.value = res.data
  } catch (err) {
    errorMsg.value = 'Failed to load weather data.'
    console.error(err)
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="p-4 text-white bg-gray-800 rounded-lg max-w-md mx-auto mt-10">
    <h2 class="text-xl font-bold mb-4">🌤️ Current Weather</h2>

    <div v-if="loading">⏳ Loading weather...</div>
    <div v-else-if="errorMsg" class="text-red-500">❌ {{ errorMsg }}</div>
    
    <div v-else>
      <p class="text-lg">{{ weather.location.name }}, {{ weather.location.country }}</p>
      <p class="text-2xl font-bold">{{ weather.current.temp_c }}°C</p>
      <p>{{ weather.current.condition.text }}</p>
      <img :src="weather.current.condition.icon" alt="weather icon" />
    </div>
  </div>
</template>
