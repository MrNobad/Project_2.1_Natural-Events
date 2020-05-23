<template lang="html">
  <div id="mapid">
    <l-map style="height: 100%; width: 90%" :zoom="zoom" :center="center" ref="map">
      <l-tile-layer :url="url">
      </l-tile-layer>
      <l-marker
      v-for="(event, index) in eventsData"
      :key="index"
      :latLng="{
        lat: event.geometries[0].coordinates[1],
        lng: event.geometries[0].coordinates[0]
        }"
        v-on:click="handleClick(event)">
        <l-popup :content="event.title"> </l-popup>
      </l-marker>
    </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker, LPopup} from 'vue2-leaflet'
import {eventBus} from '../main.js'


export default {
  name: 'map-id',
  eventsData: [],
  eventLatLng: [],
  props: ['mapid', 'eventsData'],


  components: {
    "l-map": LMap,
    "l-tile-layer": LTileLayer,
    "l-marker": LMarker,
    "l-popup": LPopup
  },
  data () {
    return {
      url: 'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      zoom: 2.5,
      center: [47.413220, -1.219482],
      markerLatLng: [47.313220, -1.319482]
    };
  },

  mounted() {
    eventBus.$on('event-selected', (event) => {
      this.zoomEvent([event.geometries[0].coordinates[0], event.geometries[0].coordinates[1]])
    })
  },

  methods: {
    handleClick(event){
      eventBus.$emit('event-selected', event)
    },

    zoomEvent(coordinates){
      if (!coordinates) {
        this.center = "center"
      }else{
        this.$refs.map.mapObject.flyTo([coordinates[1], coordinates[0]], 9);

      }
    }
  }
}
</script>

<style lang="css" scoped>
#mapid {
  height: 500px;
  justify-content: space-around;
  padding-left: 150px;
}


</style>
