<template lang="html">
  <div v-if="indEvent" id="indEventDetail">
    <h2>{{indEvent.title}}</h2>
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
