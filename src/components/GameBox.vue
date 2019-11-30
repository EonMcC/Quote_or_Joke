<template lang="html">
  <div>
    <hr>
    <h3 v-on:click="handleClick">Roll Up, Roll Up</h3>
    <hr>
    <h4>Who said the following quote?</h4>
    <p>{{realQuote.quoteText}}</p>
  </div>
</template>

<script>
export default {
  name: "game-box",
  data(){
    return{
      realQuoteMatch: null,
      realQuote: null,
      fakeQuote1: null,
      fakeQuote2: null
    };
  },
  methods: {
    handleClick(){
      fetch('https://quote-garden.herokuapp.com/quotes/random')
      .then(res => res.json())
      .then(quote => {
        this.realQuoteMatch = quote;
        this.realQuote = quote;
      })
      fetch('https://quote-garden.herokuapp.com/quotes/random')
      .then(res => res.json())
      .then(quote => this.fakeQuote1 = quote);

      fetch('https://quote-garden.herokuapp.com/quotes/random')
      .then(res => res.json())
      .then(quote => this.fakeQuote2 = quote);
    }

  }
}
</script>

<style lang="css" scoped>
</style>
