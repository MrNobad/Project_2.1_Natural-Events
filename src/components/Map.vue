<template lang="html">
  <div id="mapid">
    <l-map style="height: 80%; width: 100%" :zoom="zoom" :center="center">
      <l-tile-layer :url="url">
      </l-tile-layer>
      <l-marker
      v-for="(event, index) in eventsData"
      :key="index"
      :latLng="{
        lat: event.geometries[0].coordinates[1],
        lng: event.geometries[0].coordinates[0]
      }">
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

  },

methods: {
  // openPopup: (index) => {
  //   console.log(index);
  // }
}
}
</script>

<style lang="css" scoped>
#mapid {
  height: 500px;
}

</style>
