<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Quote</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <quote-item :quote="quoteBox"></quote-item>
        <button :quote="quoteBox" type="button" v-on:click="handleClickQuoteReload">New Quote Please!</button>
      </div>
  </transition>
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
      eventBus.$emit('faveQuoteDisplay', this.display);
        }
    }
}
</script>

<style lang="css" scoped>
  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  button {
    margin: 10px;
  }
</style>
