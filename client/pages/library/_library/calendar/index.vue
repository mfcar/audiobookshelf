<template>
  <div class="page" :class="streamLibraryItem ? 'streaming' : ''">
    <app-book-shelf-toolbar page="calendar" is-home />
    <div id="bookshelf" class="w-full h-full p-8 overflow-y-auto">
      <FullCalendar :options="calendarOptions" />
      <div>
        <div>Backup schedule</div>
        <div>Backup schedule</div>
      </div>
    </div>
  </div>
</template>

<script>

import FullCalendar from '@fullcalendar/vue'
import dayGridPlugin from '@fullcalendar/daygrid'
import timeGridPlugin from '@fullcalendar/timegrid'
import listPlugin from '@fullcalendar/list'
import interactionPlugin from '@fullcalendar/interaction'

export default {
  components: {
    FullCalendar
  },
  async asyncData({ params }) {
    const libraryId = params.library

    return {
      libraryId
    }
  },
  data() {
    return {}
  },
  computed: {
    streamLibraryItem() {
      return this.$store.state.streamLibraryItem
    },
    currentLibraryId() {
      return this.$store.state.libraries.currentLibraryId
    },
    firstDayOfWeek() {
      return this.$store.state.serverSettings.firstDayOfWeek
    },
    calendarOptions() {
      return {
        plugins: [dayGridPlugin, timeGridPlugin, interactionPlugin, listPlugin],
        headerToolbar: {
          left: 'prev,next today',
          center: 'title',
          right: 'dayGridMonth,timeGridWeek,timeGridDay,listWeek'
        },
        firstDay: this.firstDayOfWeek,
        initialView: 'dayGridMonth',
        datesSet: this.handleDatesSet
      }
    }
  },
  methods: {
    handleDatesSet(dateInfo){
      console.log("handleDatesSet handled", dateInfo);
    },
  },
  mounted() {
  }
}
</script>
