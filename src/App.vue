<template>
  <div id="app">
    <div class="header">
      <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/NASA_logo.svg/200px-NASA_logo.svg.png" alt="">
      <p class="p" ><strong>The Earth Observatory Natural Event Tracker (EONET)</strong></p>
      <h3>Powered by NASA and Stephen</h3>
    </div>
    <div class="event-wrapper">
      <ind-event-detail class:="event-item" :indEvent="selectedEvent" id="event-item" ></ind-event-detail>
    </div>
    <div class="header">
      <map-view class="map-centre" :eventsData="eventsDataFiltered" :mapid="mapid"></map-view>
      <br>

      <button id="button" type="button" v-for="(eventType, index) in eventTypes" name="eventType" @click="selectedEventType(eventType)"><strong>{{eventType}}</strong></button>
      <button id="button" type="button" name="View All" @click="selectedEventType('')"><strong>Reset Filters</strong></button>


      <event-type-description :eventTypeDescription="eventTypeDescription"></event-type-description>
    </div>
    <br>
    <event-list class="body" :eventsData="eventsDataFiltered"></event-list>

    <p>Icons made by <a href="https://www.flaticon.com/authors/freepik" title="Freepik">Freepik</a> from <a href="https://www.flaticon.com/"     title="Flaticon">www.flaticon.com</a></p>
  </div>
</template>

<script>
import {eventBus} from './main.js'
import EventDetail from './components/EventDetail.vue';
import Map from './components/Map.vue';
import EventList from './components/EventList.vue';
import EventTypeDescription from './components/EventTypeDescription'


export default {
  name: 'app',


  data() {
    return {
      mapid: [],
      eventTypes: ['Severe Storms', 'Sea and Lake Ice', 'Volcanoes', 'Wildfires'],
      eventsData: [],
      selectedEvent: null,
      eventsDataFiltered: [],
    }
  },
  props: ['eventTypeDescription'],

  components: {
    "map-view": Map,
    "event-list": EventList,
    "ind-event-detail": EventDetail,
    "event-type-description": EventTypeDescription

  },

  methods: {
    selectedEventType: function(eventType){
      if (!eventType) {
        this.eventsDataFiltered = this.eventsData
      }else{
        this.eventsDataFiltered = this.eventsData.filter((event) => {
          return event.categories[0].title === eventType;
        })}
        eventBus.$emit("event-type-selected", eventType)
      }
    },


    mounted(){
      fetch('https://eonet.sci.gsfc.nasa.gov/api/v2.1/events')
      .then(response => response.json())
      .then(res => {
        this.eventsData = res.events
        this.eventsDataFiltered = res.events})
        eventBus.$on('event-selected', (event) => this.selectedEvent = event)
        eventBus.$on('event-type-description', (event) => this.eventTypeDescription = event)

      },

    }
    </script>

    <style lang="css">
      #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        text-align: left;
        color: #000000;
        margin-top: 10px;
        padding: 25px;
      }

      .header {
        text-align: center;
        padding: 25px;
      }

      #button {
        height: 50px;
        width: auto;
        padding-left: 20px;
        padding-right: 20px;
        margin: 5px;
        border-color: salmon;
        background-color: dodgerblue;
        font-size: 20px;

      }

      .p {
        font-size: 60px;

      }

eventTypeDescription{
  display: flex;
  flex-box: wrap;
}

.event-wrapper {
  display: flex;
  flex-wrap: wrap;
}

    </style>
