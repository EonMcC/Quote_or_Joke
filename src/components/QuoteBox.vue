<template lang="html">
  <div>
    <quote-item :quote="quoteBox"></quote-item>
    <button type="button" v-on:click="handleClickQuoteReload"></button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import QuoteItem from './QuoteItem.vue';
export default {
  name: "quote-box",
  props: ['quoteBox'],
  components: {
    "quote-item": QuoteItem
  },
  methods: {
    handleClickQuoteReload(){
      eventBus.$emit('reloadQuote');
    }
  }
}
</script>

<style lang="css" scoped>
</style>
