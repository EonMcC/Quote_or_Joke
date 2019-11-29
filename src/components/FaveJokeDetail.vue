<template lang="html">
  <div v-if="faveJoke">
    <h3>{{faveJoke.setup}}</h3>
    <h4>{{faveJoke.punchline}}</h4>

  </div>
</template>

<script>
export default {
  name: "fave-joke-detail",
  props: ['faveJoke']
}
</script>

<style lang="css" scoped>
</style>
