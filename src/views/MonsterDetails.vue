<script setup>
import { onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'
import useMonsters from '@/composables/useMonsters'

const route = useRoute()
const { fetchMonster, currentMonster } = useMonsters()

onMounted(async () => {
  await fetchMonster(route.params.id)
})

onUnmounted(() => {
  currentMonster.value = null
})
</script>

<template>
  <main class="min-h-screen bg-gradient-to-r from-green-400 to-green-900 py-8 text-white">
    <div v-if="currentMonster" class="flex flex-col items-center justify-center gap-6">
      <img class="rounded-lg" :src="currentMonster.image" :alt="currentMonster.name" />
      <h1 class="text-6xl font-semibold text-yellow-100">Hi, I'm {{ currentMonster.name }}</h1>
      <pre>{{ currentMonster.common_locations }}</pre>
    </div>
  </main>
</template>
