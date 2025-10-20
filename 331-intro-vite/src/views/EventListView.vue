<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
import EventMeta from '@/components/EventMeta.vue'
import type { Event } from '@/types'
import { ref, onMounted } from 'vue'
import EventService from '@/services/EventService'

const events = ref<Event[] | null>(null)

onMounted(async () => {
  try {
    const response = await EventService.getEvents()
    events.value = response.data
  } catch (error) {
    console.error('There was an error!', error)
  }
})
</script>

<template>
  <h1>Events For Good</h1>
  <div class="events" v-if="events">
    <div v-for="event in events" :key="event.id">
      <EventCard :event="event" />
      <EventMeta :event="event" />
    </div>
  </div>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
