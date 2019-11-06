<template lang="html">
  <div v-if="indEvent" id="indEventDetail">
    <h1>Natural Event: {{indEvent.title}}</h1>
    <h2>Type: {{indEvent.categories[0].title}}</h2>
    <h3>Date: {{indEvent.geometries[0].date.slice(0, 10)}}</h3>
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
