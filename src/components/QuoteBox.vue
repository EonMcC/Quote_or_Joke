<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Quote</h3>
    <hr>
    <quote-item v-show="display" :quote="quoteBox"></quote-item>
    <button v-show="display" :quote="quoteBox" type="button" v-on:click="handleClickQuoteReload">New Quote Please!</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import QuoteItem from './QuoteItem.vue';
export default {
  name: "quote-box",
  data(){
    return {
      display: false
    };
  },
  props: ['quoteBox'],
  components: {
    "quote-item": QuoteItem
  },
  methods: {
    handleClickQuoteReload(){
      eventBus.$emit('reloadQuote');
    },
    mouseOver: function(){
      this.display = !this.display;
        }

    }

}
</script>

<style lang="css" scoped>
div {
}
</style>
