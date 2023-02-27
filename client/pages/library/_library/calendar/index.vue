<template>
  <div class="page" :class="streamLibraryItem ? 'streaming' : ''">
    <app-book-shelf-toolbar page="calendar" is-home />
    <div id="bookshelf" class="w-full h-full p-8 overflow-y-auto">
      <FullCalendar :options="calendarOptions" />
    </div>
  </div>
</template>

<script>

import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import interactionPlugin from '@fullcalendar/interaction'

export default {
  components: {
    FullCalendar
  },
  async asyncData({ params }) {
    const libraryId = params.library;

    return {
      libraryId
    }
  },
  data() {
    return {
      calendarOptions: {
        plugins: [ dayGridPlugin, interactionPlugin ],
        headerToolbar: {
          left: 'prev,next today',
          center: 'title',
          right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek'
        },
        firstDay: 0,
        initialView: 'dayGridMonth',
        events: [
          { title: 'event 1', date: '2023-02-01' },
          { title: 'event 2', date: '2023-02-02' }
        ]
      }
    }
  },
  computed: {
    streamLibraryItem() {
      return this.$store.state.streamLibraryItem
    },
    currentLibraryId() {
      return this.$store.state.libraries.currentLibraryId
    }
  },
  methods: {
  },
  mounted() {
  }
}
</script>
