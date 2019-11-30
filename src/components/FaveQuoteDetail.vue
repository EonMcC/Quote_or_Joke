<template lang="html">
  <div v-if="faveQuote">
    <p>{{faveQuote.quoteText}}</p>
    <p><strong>{{faveQuote.quoteAuthor}}</strong></p>
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
