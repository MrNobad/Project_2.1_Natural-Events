<template lang="html">
  <div v-if="indEvent" id="indEventDetail">
    <h2>Natural Event: {{indEvent.title}}</h2>
    <p>Type: {{indEvent.categories[0].title}}</p>
    <p>Date: {{indEvent.geometries[0].date.slice(0, 10)}}</p>
    <p></p>
  </div>
</template>

<script>
export default {
  name: 'ind-event-detail',
  props: ['indEvent']
}
// TODO: use .splice to show date only
</script>

<style lang="css" scoped>
</style>
