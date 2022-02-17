<template>
  <div
    class="relative flex items-top justify-center min-h-screen bg-gray-100 sm:items-center sm:pt-0"
  >
   <h1>
     Event
   </h1>

       <EventCard
      v-for="(event, index) in events"
      :key="index"
      :event="event"
      :data-index="index"
    />
 </div>
</template>

<script>
import { mapState } from 'vuex'

import EventCard from '@/components/EventCard.vue'

export default {
  name: 'IndexPage',
  components: {
    EventCard,
  },

  // async fetch({ store, error }) {
  //   try {
  //     await store.dispatch('events/fetchEvents')
  //   } catch (e) {
  //     error({
  //       statusCode: 503,
  //       message: 'Unable to fetch events at this time. Please try again.',
  //     })
  //   }
  // },

  async fetch({ store, error }) {
    try {
      await store.dispatch('events/fetchEvents')
      // $axios.get('http://localhost:3000/events')
    } catch (e) {
      error({
        statusCode: 503,
        message:
          'Unable to retrive the data. Please try again later hooouuuuu.',
      })
    }
  },

  head() {
    return {
      title: 'Event Listening ',
    }
  },
  computed: mapState({
    events: (state) => state.events.events,
  }),
}
</script>
