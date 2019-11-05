<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <h2>Event</h2>

    <map-view :eventsData="eventsData" :mapid="mapid"></map-view>
    <event-list :eventsData="eventsData"></event-list>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import NaturalEvent from './components/NaturalEvent.vue';
import Map from './components/Map.vue';
import EventList from './components/EventList.vue'


export default {
  name: 'app',
  props: ['indEvent'],

  data() {
    return {
      mapid: [],
      eventsData: []
    }
  },
  components: {
    "map-view": Map,
    "event-list": EventList

  },

  mounted(){
    fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
    .then(response => response.json())
    .then(res => {
      this.eventsData = res.events
    eventBus.$on('event-selected', this.indEvent)
    })
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
