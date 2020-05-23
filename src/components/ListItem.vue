<template lang="html">
  <div class="">
    <li v-on:click="handleClick">{{indEvent.title}}</li>
  </div>
</template>

<script>
import {eventBus} from '../main.js'


export default {
  name: 'list-item',
  props: ['indEvent'],
  methods: {
    handleClick(){
      eventBus.$emit('event-selected', this.indEvent)
    }

  }

}
</script>

<style lang="css" scoped>
</style>
