<template lang="html">
  <div v-if="selectedEventTypeDescription">
    <img :src="selectedEventTypeDescription.url" alt="">
    <h2>{{selectedEventTypeDescription.title}}</h2>
    <p>{{selectedEventTypeDescription.info}}</p>
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: "event-types-description",


  data(){
    return {
      selectedEventTypeDescription: {},
      eventTypesDescription: [{
        "title": "Severe Storms",
        "info": "A typhoon is a mature tropical cyclone that develops between 180° and 100°E in the Northern Hemisphere. This region is referred to as the Northwestern Pacific Basin,[1] and is the most active tropical cyclone basin on Earth, accounting for almost one-third of the world's annual tropical cyclones. For organizational purposes, the northern Pacific Ocean is divided into three regions: the eastern (North America to 140°W), central (140°W to 180°), and western (180° to 100°E). The Regional Specialized Meteorological Center (RSMC) for tropical cyclone forecasts is in Japan, with other tropical cyclone warning centers for the northwest Pacific in Hawaii (the Joint Typhoon Warning Center), the Philippines and Hong Kong. While the RSMC names each system, the main name list itself is coordinated among 18 countries that have territories threatened by typhoons each year.",
        "url": "/assets/014-tornado.png"
      },
      {"title": "Wildfires",
      "info": "A wildfire, wildland fire or rural fire is an uncontrolled fire in an area of combustible vegetation occurring in rural areas. Depending on the type of vegetation present, a wildfire can also be classified more specifically as a brush fire, bushfire, desert fire, forest fire, grass fire, hill fire, peat fire, vegetation fire, or veld fire. Many organizations consider wildfire to mean an unplanned and unwanted fire, while wildland fire is a broader term that includes prescribed fire as well as wildland fire use (WFU; these are also called monitored response fires).",
      "url": "/assets/019-forest-fire-1.png"
    },
      {"title": "Sea and Lake Ice",
      "info": "An iceberg is a large piece of freshwater ice that has broken off a glacier or an ice shelf and is floating freely in open (salt) water. Small bits of disintegrating icebergs are called 'growlers' or 'bergy bits'. Much of an iceberg is below the surface which gave buoyancy to the expression 'tip of the iceberg' to illustrate a small part of a larger unseen issue. Icebergs are considered a serious maritime hazard. The 1912 loss of the 'unsinkable' RMS Titanic led to the formation of the International Ice Patrol in 1914. Icebergs calved by glaciers that face the open sea, such as in Greenland, are irregular shaped piles. In Antarctica, ice shelves calve large tabular (table top) icebergs. The biggest iceberg ever recorded was Iceberg B-15A which split off the Ross Ice Shelf in Antarctica in 2000.",
      "url": "/assets/007-glacier.png"
    },
      {"title": "Volcanoes",
      "info": "A volcano is a rupture in the crust of a planetary-mass object, such as Earth, that allows hot lava, volcanic ash, and gases to escape from a magma chamber below the surface. Earth's volcanoes occur because its crust is broken into 17 major, rigid tectonic plates that float on a hotter, softer layer in its mantle. Therefore, on Earth, volcanoes are generally found where tectonic plates are diverging or converging, and most are found underwater. For example, a mid-oceanic ridge, such as the Mid-Atlantic Ridge, has volcanoes caused by divergent tectonic plates whereas the Pacific Ring of Fire has volcanoes caused by convergent tectonic plates. Volcanoes can also form where there is stretching and thinning of the crust's plates, e.g., in the East African Rift and the Wells Gray-Clearwater volcanic field and Rio Grande Rift in North America. This type of volcanism falls under the umbrella of 'plate hypothesis' volcanism. Volcanism away from plate boundaries has also been explained as mantle plumes. These so-called 'hotspots', for example Hawaii, are postulated to arise from upwelling diapirs with magma from the core–mantle boundary, 3,000 km deep in the Earth. Volcanoes are usually not created where two tectonic plates slide past one another.",
      "url": "/assets/002-eruption.png"
    }
    ]}
  },
props: ['eventsData'],
mounted(){
  eventBus.$on("event-type-selected", (eventType)=>{
    this.setEventDescription(eventType)
  })
},

  methods: {
    setEventDescription(eventType){
      if (!eventType) { ""
      }else{
      this.selectedEventTypeDescription = this.eventTypesDescription.find((eventDescription) => {
        return eventDescription.title === eventType;
      })}
  }
}
}
</script>

<style lang="css" scoped>
 h3, p, img {
display: flex-box;
flex-wrap: wrap;
}

img {
  height: 100px;
  padding: 15px;
}
</style>
