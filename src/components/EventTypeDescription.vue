<template lang="html">
  <div v-if="selectedEventTypeDescription">
    <h3>{{selectedEventTypeDescription.title}}</h3>
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
        "info": "Not nice weather",
        "url": "https.//something"
      },
      {"title": "Wildfires",
      "info": "It's getting hot",
      "url": "https.//something"}
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
</style>
