<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <h2>Event</h2>
    <ind-event-detail :indEvent="selectedEvent"></ind-event-detail>
    <map-view :eventsData="eventsDataFiltered" :mapid="mapid"></map-view>
    <event-type-description :eventTypeDescription="eventTypeDescription"></event-type-description>
    <button type="button" v-for="(eventType, index) in eventTypes" name="eventType" @click="filteredEvents(eventType)">{{eventType}}</button>

    <!-- <button type="button" name="Severe Storms" @click="filteredEvents('Severe Storms')">Severe Storms</button>
    <button type="button" name="Icebergs" @click="filteredEvents('Sea and Lake Ice')">Icebergs</button>
    <button type="button" name="Volcanoes" @click="filteredEvents('Volcanoes')">Volcanoes</button>
    <button type="button" name="Wildfires" @click="filteredEvents('Wildfires')">Wildfires</button> -->
    <button type="button" name="View All" @click="filteredEvents('')">Reset Filters</button>

    <event-list :eventsData="eventsDataFiltered"></event-list>
    <h3>Icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/"     title="Flaticon">www.flaticon.com</a></h3>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import EventDetail from './components/EventDetail.vue';
import Map from './components/Map.vue';
import EventList from './components/EventList.vue';
// import EventTypeDescription from './components/EventTypeDescription'


export default {
  name: 'app',
  // props: ['indEvent'],

  data() {
    return {
      mapid: [],
      eventTypes: ['Severe Storms', 'Sea and Lake Ice', 'Volcanoes', 'Wildfires'],
      eventsData: [],
      selectedEvent: null,
      eventsDataFiltered: [],
      eventTypeDescription: ""
    }
  },
  components: {
    "map-view": Map,
    "event-list": EventList,
    "ind-event-detail": EventDetail,
    // "event-type-description": eventTypeDescription
    // "filtered-events": FilteredEvents

  },

  methods: {
    filteredEvents: function(value){
      if (!value) {
        this.eventsDataFiltered = this.eventsData
      }else{
      this.eventsDataFiltered = this.eventsData.filter((event) => {
        return event.categories[0].title === value;
      })}


    }
  },


  mounted(){
    fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
    .then(response => response.json())
    .then(res => {
      this.eventsData = res.events
      this.eventsDataFiltered = res.events})
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
