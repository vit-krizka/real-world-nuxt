<template>
  <div>
    <h1>Events</h1>
    <EventCard v-for="(event, index) in events" :key="index" :event="event" :data-index="index">
    </EventCard>
  </div>
</template>

<script>
import { mapState } from 'vuex'
import EventCard from '@/components/EventCard.vue'

export default {
  name: 'IndexPage',
  head() {
    return {
      title: 'Event Listing'
    }
  },
  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
    } catch (e) {
      error({
        statusCode: 503,
        message: 'Unable to fetch events events at this time'
      })
    }
  },
  components: {
    EventCard
  },
  computed: mapState({
    events: state => state.events.events
  })
}
</script>
