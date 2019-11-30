<template lang="html">
  <div v-if="joke">
    <p>{{this.joke.setup}}</p>
    <p><strong>{{this.joke.punchline}}</strong></p>
    <button type="button" v-on:click="handleClickFave">Save as a Fave</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js';
export default {
  name: "joke-item",
  props: ['joke'],
  methods: {
    handleClickFave(){
      eventBus.$emit('selected-fave-joke', this.joke);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
