<template lang="html">
  <div>
    <p>{{quote.quoteText}}</p>
    <p>~ {{quote.quoteAuthor}} ~</p>
    <button type="button" v-on:click="handleClickFave">Save as a Fave</button>
  </div>

</template>

<script>
import {eventBus} from '../main.js';
export default {
  name: "quote-detail",
  props: ['quote'],
  methods: {
    handClickFave(){
      eventBus.$emit('selected-fave-quote', this.quote);
    }
  }
}
</script>

<style lang="css" scoped>
</style>
