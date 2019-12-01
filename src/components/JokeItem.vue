<template lang="html">
  <div v-if="joke">
    <p>{{this.joke.setup}}</p>
    <p v-if="displayPunchline === true"><strong>{{this.joke.punchline}}</strong></p>
    <p class="click" v-on:click="handleClickPunchline">(click to reveal/hide punchline)</p>
    <button type="button" v-on:click="handleClickFave">Save as a Fave</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js';
export default {
  name: "joke-item",
  data(){
    return {
      displayPunchline: false
    };
  },
  props: ['joke'],
  methods: {
    handleClickFave(){
      eventBus.$emit('selected-fave-joke', this.joke);
    },
    handleClickPunchline(){
      this.displayPunchline = !this.displayPunchline;
  }
}
}
</script>

<style lang="css" scoped>
  .click {
    cursor: pointer;
    font-size: 0.5em;
  }

</style>
