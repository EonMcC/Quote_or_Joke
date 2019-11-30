<template lang="html">
  <div v-if="quote">
    <p>{{quote.quoteText}}</p>
    <p><strong>~ {{quote.quoteAuthor}} ~</strong></p>
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
