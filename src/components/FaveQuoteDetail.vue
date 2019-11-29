<template lang="html">
  <div v-if="faveQuote">
    <h3>{{faveQuote.quoteText}}</h3>
    <h4>{{faveQuote.quoteAuthor}}</h4>

  </div>
</template>

<script>
export default {
  name: "fave-quote-detail",
  props: ['faveQuote']
}
</script>

<style lang="css" scoped>
</style>
