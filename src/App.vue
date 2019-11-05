<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <h2>Event</h2>
    <ind-event-detail :indEvent="selectedEvent"></ind-event-detail>
    <map-view :eventsData="eventsData" :mapid="mapid"></map-view>
    <button type="button" name="Severe Storms" value="Severe Storms" @click="filteredEvents('Severe Storms')">Severe Storms</button>
    <button type="button" name="Icebergs" @click="filteredEvents('Sea and Lake Ice')">Icebergs</button>
    <button type="button" name="Volcanoes" @click="filteredEvents()">Volcanoes</button>
    <button type="button" name="Wildfires" @click="filteredEvents()">Wildfires</button>
    <!-- <filtered-events>
      <select id="event-select" v-model="eventsData">
        <option v-for="(event, title) in eventsData" :value="event">{{title}}</option>
      </select>
    </filtered-events> -->
    <event-list :eventsData="eventsData"></event-list>
    <h3>Icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/"     title="Flaticon">www.flaticon.com</a></h3>
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
      selectedEvent: null,
      // filteredEvents: null
    }
  },
  components: {
    "map-view": Map,
    "event-list": EventList,
    "ind-event-detail": EventDetail,
    // "filtered-events": FilteredEvents

  },

  methods: {
    filteredEvents: function(value){
      this.eventsData = this.eventsData.filter((event) => {
        return event.categories[0].title === value;
      })
    }

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
