<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Roll Up, Roll Up</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <button type="button" v-on:click="generate">Generate/Reset Game</button>
        <h4>Who said the following quote?</h4>
        <h3 v-if="realQuote">{{this.realQuote.quoteText}}</h3>
        <h1 class="wrong" v-if="lose">Wrong</h1>
        <h1 class="correct" v-if="win">Correct!</h1>
        <div class="answer-container">
          <p v-for="quote in threeQuotes" v-on:click="winLose(quote)">
            {{quote.quoteAuthor}}
          </p>
          <!-- <p style="order:" v-if="realQuote" v-on:click="youWin">{{this.realQuote[0].quoteAuthor}}</p> -->
          <!-- <p :style="`order:{{randomIndex(allQuotes)}};`" v-if="fakeQuote1" v-on:click="youLose">{{this.fakeQuote1[0].quoteAuthor}}</p>
          <p :style="`order:{{randomIndex(allQuotes)}};`" v-if="fakeQuote2" v-on:click="youLose">{{this.fakeQuote2[0].quoteAuthor}}</p> -->
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
      this.threeQuotes = [];
      for (i = 0; i < 3; i++) {
        this.threeQuotes.push(this.allQuotes[this.randomIndex(this.allQuotes)]);
      }
      this.realQuote = this.threeQuotes[this.randomIndex(this.threeQuotes)];
      // this.realQuote = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);

      // this.fakeQuote1 = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);
      //
      // this.fakeQuote2 = this.threeQuotes.splice(this.allQuotes[this.randomIndex(this.allQuotes)], 1);

      this.lose = false;
      this.win = false;
    },
    winLose(e){
      if (e === this.realQuote) {
        this.win = true;
      } else {
        this.lose = true;

      }
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
