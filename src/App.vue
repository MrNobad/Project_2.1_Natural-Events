<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <h2>Event</h2>
    <ind-event-detail :indEvent="selectedEvent"></ind-event-detail>
    <map-view :eventsData="eventsData" :mapid="mapid"></map-view>
    <event-list :eventsData="eventsData"></event-list>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import EventDetail from './components/EventDetail.vue';
import Map from './components/Map.vue';
import EventList from './components/EventList.vue'


export default {
  name: 'app',
  // props: ['indEvent'],

  data() {
    return {
      mapid: [],
      eventsData: [],
      selectedEvent: null
    }
  },
  components: {
    "map-view": Map,
    "event-list": EventList,
    "ind-event-detail": EventDetail

  },

  mounted(){
    fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
    .then(response => response.json())
    .then(res => {
      this.eventsData = res.events})
    eventBus.$on('event-selected', (event) => this.selectedEvent = event)

  },


  filters: {

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: left;
  color: #000000;
  margin-top: 60px;
}
</style>
