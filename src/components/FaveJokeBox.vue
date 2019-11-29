<template lang="html">
  <div>
    <ul>
      <fave-joke-detail v-for="(fave, index) in faveJokes" :faveJoke="fave" :key="index"></fave-joke-detail>
    </ul>

  </div>
</template>

<script>
import FaveJokeDetail from './FaveJokeDetail.vue';

export default {
  name: "fave-joke-box",
  props: ['faveJokes'],
  components: {
    "fave-joke-detail": FaveJokeDetail
  }
}
</script>

<style lang="css" scoped>
</style>
