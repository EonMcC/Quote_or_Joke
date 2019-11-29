<template lang="html">
  <div v-if="joke">
    <p>{{this.joke.setup}}</p>
    <p>{{this.joke.punchline}}</p>
  </div>
</template>

<script>
export default {
  name: "joke-item",
  props: ['joke']
}
</script>

<style lang="css" scoped>
</style>
