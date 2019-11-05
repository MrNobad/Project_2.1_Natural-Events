<template lang="html">
  <div v-if="handleClick">
    <p>{{eventTypeDescription.description}}</p>
  </div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
name: "event-type-description",
props: ["eventTypeDescription"],
methods: {
  eventBus.$emit('event-type-description', this.eventTypeDescription)
},

  data(){
    return {
      "Severe Storm": "Not nice weather",
      "Wildfires": "It's getting hot"
    }
  }
}
</script>

<style lang="css" scoped>
</style>
