<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Roll Up, Roll Up</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <button type="button" v-on:click="generate">Generate/Reset Game</button>
        <h4>Who said the following quote?</h4>
        <h3 v-if="realQuote">{{this.realQuote[0].quoteText}}</h3>
        <h1 v-if="lose">Wrong</h1>
        <h1 v-if="win">Correct!</h1>
        <div class="answer-container">
          <p v-if="realQuote" v-on:click="youWin">{{this.realQuote[0].quoteAuthor}}</p>
          <p v-if="fakeQuote1" v-if:click="youLose">{{this.fakeQuote1[0].quoteAuthor}}</p>
          <p v-if="fakeQuote2" v-on:click="youLose">{{this.fakeQuote2[0].quoteAuthor}}</p>
        </div>
    </div>
  </transition>
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
      fakeQuote2: null,
      win: false,
      lose: false,
      display: false
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

      this.lose = false;
      this.win = false;
    },

    youLose(){
      this.lose = true;
    },
    youWin(){
      this.win = true;
    },
    mouseOver: function(){
    this.display = !this.display;
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
    cursor: pointer;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

</style>
