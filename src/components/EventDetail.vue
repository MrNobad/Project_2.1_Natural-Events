<template lang="html">
  <div v-if="indEvent" id="indEventDetail">
    <h2>Natural Event: {{indEvent.title}}</h2>
    <p>Type: {{indEvent.categories[0].title}}</p>
    <p>Date: {{indEvent.geometries[0].date.slice(0, 10)}}</p>
  <!-- <p><iframe :src="indEvent.sources[0].url" width="300px" height="100px"></iframe></p> -->
  </div>
</template>

<script>
export default {
  name: 'ind-event-detail',
  props: ['indEvent']
}
</script>

<style lang="css" scoped>
</style>
