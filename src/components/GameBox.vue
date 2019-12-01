<template lang="html">
  <div>
    <hr>
    <h3>Roll Up, Roll Up</h3>
    <hr>
    <h4>Who said the following quote?</h4>
    <p v-if="threeQuotes.length !== 0">Test: {{this.threeQuotes[1].quoteText}}</p>
    <button type="button" v-on:click="generate">Generate Game</button>
    <h3 v-if="realQuote">{{this.realQuote[0].quoteAuthor}}</h3>
    <div class="answer-container">
      <p v-if="realQuote">{{this.realQuote[0].quoteAuthor}}</p>
      <p v-if="fakeQuote1">{{this.fakeQuote1[0].quoteAuthor}}</p>
      <p v-if="fakeQuote2">{{this.fakeQuote2[0].quoteAuthor}}</p>
    </div>
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
      var i;
      for (i = 0; i < 3; i++) {
        this.threeQuotes.push(this.allQuotes[this.randomIndex(this.allQuotes)]);
      }
      this.realQuote = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);

      this.fakeQuote1 = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);

      this.fakeQuote2 = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);
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
    border: solid 1px black;
    padding: 5px;
  }

</style>
