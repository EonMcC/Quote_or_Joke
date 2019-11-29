<template lang="html">
  <div>
    <p>{{this.quote.quoteText}}</p>
    <p>~ {{this.quote.quoteAuthor}} ~</p>
    <button type="button" v-on:click="handleClickFave">Save as a Fave</button>
  </div>

</template>

<script>
import {eventBus} from '../main.js';
export default {
  name: "quote-item",
  props: ['quote'],
  methods: {
    handleClickFave(){
      eventBus.$emit('selected-fave-quote', this.quote);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
