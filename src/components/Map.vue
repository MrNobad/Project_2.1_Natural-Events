<template lang="html">
  <div id="mapid">
    <l-map ref="myMap">
      <!-- <l-marker
      class="marker"
      v-for="(marker, index) in eventLatLng"
      :key="index"
      :latLng="marker.coordinates">
    </l-marker> -->
    </l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker} from 'vue2-leaflet'
import {eventBus} from '../main.js'


export default {
  name: 'map-id',
  props: ['mapid', "eventLatLng"],


  components: {
    "l-map": LMap,
    "l-tile-layer": LTileLayer,
    "l-marker": LMarker
  },

  mounted() {
    this.myMap = L.map('mapid').setView([51.505, -0.09], 2.3);


    L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', {
      attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
      maxZoom: 20,
      id: 'mapbox.streets',
      accessToken: process.env.VUE_APP_ACCESS_TOKEN
    }).addTo(this.myMap);


    // L.marker([33.9, -117.5]).addTo(this.myMap)
    // TODO Check if we can get rid of the bus.on
    eventBus.$on('event-coordinates-loaded', ()=>{
      this.eventLatLng.forEach((event) => {
        L.marker([event[1], event[0]]).addTo(this.myMap)
        .bindPopup('<strong>Science Hall</strong><br>Where the GISC was born.')
        .on("click", ()=>{
          openPopup()
        })
      })
    })
    // set up event bus listener, call function/callback for generationg markers with eventLatLng
  }

}
</script>

<style lang="css" scoped>
#mapid {
  height: 500px;
}

</style>
