<template lang="html">
  <div class="">
    <li v-on:click="handleClick">{{event.title}}</li>
  </div>
</template>

<script>
import {eventBus} from '../main.js'


export default {
  name: 'list-item',
  props: ['event'],
  methods: {
    handleClick(){
      eventBus.$emit('event-selected', this.event)
    }
  }

}
</script>

<style lang="css" scoped>
</style>
