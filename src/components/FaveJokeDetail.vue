<template lang="html">
  <div v-if="faveJoke">
    <p>{{faveJoke.setup}}</p>
    <p><strong>{{faveJoke.punchline}}</strong></p>

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
