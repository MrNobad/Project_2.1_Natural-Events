<template lang="html">
  <div class="event-list">
    <ul>
      <list-item
      v-for="(indEvent, index) in eventsData" :indEvent="indEvent" :key="index">
      </list-item>
    </ul>
  </div>
</template>

<script>
import ListItem from './ListItem.vue'

export default {
  name: 'events-list',
  props: ['eventsData'],

  components: {
    'list-item': ListItem
  }
}
</script>

<style lang="css" scoped>
</style>
