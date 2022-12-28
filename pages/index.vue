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
  // ES6 destructuring (context.$axios)
  asyncData({ $axios, error }) {
    return $axios.get("http://localhost:3000/events").then(response => {
      return {
        events: response.data
      }
    }).catch(e => {
      error({ statusCode: 503, message: 'Unable to fetch events at the moment. Please try again.' })
    })
  },
  // asyncDate(context) {
  //   return context.$axios.get("http://localhost:3000/events").then(response => {
  //     return {
  //       events: response.data
  //     }
  //   })
  // }
  components: {
    EventCard
  }
}
</script>
