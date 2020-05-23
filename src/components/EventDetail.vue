<template lang="html">
  <div class="event-item" v-if="indEvent" id="indEventDetail">
    <h1>Natural Event: {{indEvent.title}}</h1>
    <h2>Type: {{indEvent.categories[0].title}}</h2>
    <h3>Date: {{indEvent.geometries[0].date.slice(0, 10)}}</h3>
  </div>
</template>

<script>
export default {
  name: 'ind-event-detail',
  props: ['indEvent']
}
</script>

<style lang="css" scoped>

.event-item {
  background-color: #6495ed;
  border: 1px solid black;
  border-radius: 5px;
  padding: 20px;
  margin: 10px;
}
</style>
