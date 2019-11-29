<template lang="html">
  <div>
    <quote-item :quote="quoteBox"></quote-item>
  </div>
</template>

<script>
import QuoteItem from './QuoteItem.vue';
export default {
  name: "quote-box",
  props: ["quoteBox"],
  components: {
    "quote-item": QuoteItem
  }
}
</script>

<style lang="css" scoped>
</style>
