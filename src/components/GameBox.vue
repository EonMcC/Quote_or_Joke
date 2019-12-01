<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Roll Up, Roll Up</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <button type="button" v-on:click="generate">Generate/Reset Game</button>
        <h5>Who said the following quote?</h5>
        <h3 v-if="realQuote">"{{this.realQuote.quoteText}}"</h3>
        <h1 class="wrong" v-if="winOrLose === 0">Wrong</h1>
        <h1 class="correct" v-if="winOrLose === 1">Correct!</h1>
        <div class="answer-container">
          <p v-for="quote in threeQuotes" v-on:click="winLose(quote)">
            {{quote.quoteAuthor}}
          </p>
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
      realQuote: null,
      fakeQuote1: null,
      fakeQuote2: null,
      winOrLose: 2,
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
      this.threeQuotes = [];
      for (i = 0; i < 3; i++) {
        this.threeQuotes.push(this.allQuotes[this.randomIndex(this.allQuotes)]);
      }
      this.realQuote = this.threeQuotes[this.randomIndex(this.threeQuotes)];

      this.winOrLose = 2;
    },
    winLose(e){
      if (e === this.realQuote) {
        this.winOrLose = 1;
      } else {
        this.winOrLose = 0;
      }
    },

    youLose(){
      this.winOrLose = 0;
    },
    youWin(){
      this.winOrLose = 1;
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

  p:hover {
    margin-left: 10px;
    margin-right: 10px;
    border: solid 1px black;
    padding: 5px;
    cursor: pointer;
    background-color: #76ae76;
  }

  .correct {
    color: #76ae76;
  }

  .wrong {
    color: #6C0E23;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

</style>
