<template lang="html">
  <div>
    <fave-joke-detail class="fit-width" v-for="(fave, index) in faveJokes" :faveJoke="fave" :key="index"></fave-joke-detail>
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
.fit-width {
  width: 47%;
  padding: 5px;
}
</style>
