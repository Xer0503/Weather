<script setup>
    const { todo } = defineProps({
        todo : {
            type : Object,
            required : true
        }
    })
</script>

<template>
    <div class="p-4 bg-white rounded shadow">
        <h2 class="text-lg">{{ todo.title }}</h2>
        <p v-if="todo.completed == true" class="text-sm text-green-700 font-bold">
            Completed
        </p>
        <p v-else class="text-sm text-yellow-600 font-bold">
            Pending
        </p>
    </div>
</template>