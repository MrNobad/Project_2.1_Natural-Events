<template>
  <div id="app">
    <h1>Natural Events</h1>
    <h2>The Earth Observatory Natural Event Tracker (EONET)</h2>
    <h2>Event</h2>
    <map-view :mapid="mapid"></map-view>

  </div>
</template>

<script>
import {eventBus} from './main.js'
import NaturalEvent from './components/NaturalEvent.vue';
import Map from './components/Map.vue';


export default {
  name: 'app',

  data() {
    return {
      eventData: [],
      mapid: []

    }
  },
  components: {
    "map-view": Map
  },

  mounted(){
    fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
    .then(response => response.json())
    .then(res => this.eventData = this.transformEvents(res.events))
    // .then(res => this.eventData = this.transformEvents(res.events.description))


  },
  methods: {
    transformEvents(arr){
      return arr.map((event) => {
        return (event)
      })
    }
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
