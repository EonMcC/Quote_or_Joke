<template lang="html">
  <div>
    <hr>
    <h3>Roll Up, Roll Up</h3>
    <hr>
    <h4>Who said the following quote?</h4>
    <p v-if="threeQuotes.length !== 0">{{this.threeQuotes[1].quoteText}}</p>
    <button type="button" v-on:click="generate"></button>
    <!-- <h6 v-if="realQuote">{{this.realQuote.quoteText}}</h6> -->
    <!-- <div class="answer-container">
      <p v-if="realQuote">{{this.realQuote.quoteAuthor}}</p>
      <p v-if="fakeQuote1">{{this.fakeQuote1.quoteAuthor}}</p>
      <p v-if="fakeQuote2">{{this.fakeQuote2.quoteAuthor}}</p>
    </div> -->
  </div>
</template>

<script>
export default {
  name: "game-box",
  data(){
    return{
      allQuotes: [],
      threeQuotes: [],
      realQuoteMatch: null,
      realQuote: null,
      fakeQuote1: null,
      fakeQuote2: null
    };
  },
  mounted() {
      fetch('https://quote-garden.herokuapp.com/quotes/all')
      .then(res => res.json())
      .then(quotes => this.allQuotes = quotes.results)
  },
  methods: {
    randomIndex(array){
      let randomIndex = Math.floor(Math.random()* array.length);
      return randomIndex;
    },
    generate: function (){
      // this.threeQuotes = this.allQuotes[1].quoteText;
    var i;
    for (i = 0; i < 3; i++) {
      this.threeQuotes.push(this.allQuotes[this.randomIndex(this.allQuotes)]);
    }
  }
  }
}
</script>

<style lang="css" scoped>
  .answer-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }

  p {
    margin-left: 10px;
    margin-right: 10px;
    border: solid 2px black;
    padding: 5px;
  }

</style>
