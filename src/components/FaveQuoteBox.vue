<template lang="html">
  <div>
    <ul>
      <fave-quote-detail v-for="(fave, index) in faveQuotes" :faveQuote="fave" :key="index"></fave-quote-detail>
    </ul>

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
</style>
