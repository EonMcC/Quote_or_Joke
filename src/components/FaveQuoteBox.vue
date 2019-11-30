<template lang="html">
  <div>
    <fave-quote-detail class="fit-width" v-for="(fave, index) in faveQuotes" :faveQuote="fave" :key="index"></fave-quote-detail>
  </div>
</template>

<script>
import FaveQuoteDetail from './FaveQuoteDetail.vue';

export default {
  name: "fave-quote-box",
  props: ['faveQuotes'],
  components: {
    "fave-quote-detail": FaveQuoteDetail
  }
}
</script>

<style lang="css" scoped>
  .fit-width {
    width: 47%;
    padding: 5px;
  }
</style>
