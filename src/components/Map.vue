<template lang="html">
  <div id="mapid">
    <l-map ref="myMap"></l-map>
  </div>
</template>

<script>
import {LMap, LTileLayer, LMarker} from 'vue2-leaflet'


export default {
  name: 'map-id',
  props: ['mapid'],

  components: {
    "l-map": LMap,
    "l-tile-layer": LTileLayer,
    "l-marker": LMarker
  },

   mounted() {
     this.myMap = L.map('mapid').setView([51.505, -0.09], 13);

  L.tileLayer('https://api.tiles.mapbox.com/v4/{id}/{z}/{x}/{y}.png?access_token={accessToken}', {
	attribution: 'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
	maxZoom: 18,
	id: 'mapbox.streets',
	accessToken: process.env.VUE_APP_ACCESS_TOKEN
}).addTo(this.myMap);
   }

}
</script>

<style lang="css" scoped>
#mapid {
  height: 280px;
}
</style>
