<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" :data-index="index">
    </EventCard>
  </div>
</template>

<script>
import EventCard from '@/components/EventCard.vue'
export default {
  name: 'IndexPage',
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async asyncData({ $axios, error }) {
    try {
      const response = await $axios.get("http://localhost:3000/events");
      return {
        events: response.data
      }
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events events at this time'
      })
    }
  },
  components: {
    EventCard
  }
}
</script>
