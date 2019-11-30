<template>
  <div id="app">
    <div class="background-joker">
    </div>
    <div class="background-buddha">
    </div>
    <h1 class="app-header">Quote or Joke?</h1>
    <quote-box id="quote-box" :quoteBox="currentQuote"></quote-box>
    <transition name="fade">
      <fave-quote-box v-show="faveQuoteDisplay" id="fave-quote-box" :faveQuotes="faveQuotes"></fave-quote-box>
    </transition>
    <joke-box id="joke-box" :joke="currentJoke"></joke-box>
    <transition name="fade">
      <fave-joke-box v-show="faveJokeDisplay" id="fave-joke-box" :faveJokes="faveJokes"></fave-joke-box>
    </transition>
    <combo-box id="combo-box" :comboQuote="comboQuote" :comboJoke="comboJoke"></combo-box>
  </div>
</template>

<script>
import {eventBus} from './main.js';
import QuoteBox from './components/QuoteBox.vue';
import QuoteItem from './components/QuoteItem.vue';
import FaveQuoteBox from './components/FaveQuoteBox.vue';
import FaveQuoteDetail from './components/FaveQuoteDetail.vue';
import JokeBox from './components/JokeBox.vue';
import JokeItem from './components/JokeItem.vue';
import FaveJokeBox from './components/FaveJokeBox.vue';
import FaveJokeDetail from './components/FaveJokeDetail.vue';
import ComboBox from './components/ComboBox.vue';

export default {
  name: 'app',
  data(){
    return {
      quotes: [],
      jokes:[],
      currentQuote: null,
      faveQuotes: [],
      currentJoke: null,
      faveJokes: [],
      comboQuote: null,
      comboJoke: null,
      faveQuoteDisplay: false,
      faveJokeDisplay: false

    };
},
mounted(){
  fetch('https://quote-garden.herokuapp.com/quotes/random')
  .then(res => res.json())
  .then(quote => {
    this.quotes.push(quote);
    this.currentQuote = quote;
  })

  fetch('https://official-joke-api.appspot.com/random_joke')
  .then(res => res.json())
  .then(joke => {
    this.jokes.push(joke);
    this.currentJoke = joke;
  })

  eventBus.$on('selected-fave-quote', (faveQuote) => {
    this.faveQuotes.push(faveQuote);
  })
  eventBus.$on('selected-fave-joke', (faveJoke) => {
    this.faveJokes.push(faveJoke);
  })
  eventBus.$on('reloadQuote', () => {
    fetch('https://quote-garden.herokuapp.com/quotes/random')
    .then(res => res.json())
    .then(quote => {
      this.quotes.push(quote);
      this.currentQuote = quote;
    })
  })
  eventBus.$on('reloadJoke', () => {
    fetch('https://official-joke-api.appspot.com/random_joke')
    .then(res => res.json())
    .then(joke => {
      this.jokes.push(joke);
      this.currentJoke = joke;
    })
  })
  eventBus.$on('loadCombo', () => {
    fetch('https://official-joke-api.appspot.com/random_joke')
    .then(result => result.json())
    .then(joke => this.comboJoke = joke.punchline);
    fetch('https://quote-garden.herokuapp.com/quotes/random')
    .then(res => res.json())
    .then(quote => this.comboQuote = quote.quoteAuthor);
    })
    eventBus.$on('faveQuoteDisplay', (status) => {
      this.faveQuoteDisplay = status;
    })
    eventBus.$on('faveJokeDisplay', (status) => {
      this.faveJokeDisplay = status;
    })
},
components: {
  "quote-box": QuoteBox,
  "quote-item": QuoteItem,
  "fave-quote-box": FaveQuoteBox,
  "fave-quote-detail": FaveQuoteDetail,
  "joke-box": JokeBox,
  "fave-joke-box": FaveJokeBox,
  "fave-joke-detail": FaveJokeDetail,
  "combo-box": ComboBox
}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 40px;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  grid-template-rows: 125px 300px auto 300px;
}

.app-header {
  grid-column-start: 5;
  grid-column-end: 9;
}

#quote-box {
  grid-row-start: 2;
  grid-row-end: 3;
  grid-column-start: 2;
  grid-column-end: 6;
}

#fave-quote-box {
  grid-row-start: 3;
  grid-row-end: 4;
  grid-column-start: 2;
  grid-column-end: 6;
  display: flex;
  flex-wrap: wrap;
}

#joke-box {
  grid-row-start: 2;
  grid-row-end: 3;
  grid-column-start: 8;
  grid-column-end: 12;
}

#fave-joke-box {
  grid-row-start: 3;
  grid-row-end: 4;
  grid-column-start: 8;
  grid-column-end: 12;
  display: flex;
  flex-wrap: wrap;
}

#combo-box {
  grid-row-start: 4;
  grid-row-end: 5;
  grid-column-start: 4;
  grid-column-end: 10;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity 1s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}

.background-joker {
  background-image: url(../public/images/joker.jpg);
  background-position: center;
  opacity: 0.1;
  z-index: -1;
  overflow: hidden;
  position: absolute;
  height: 100vh;
  width: 300px;
  right: 0;
}

.background-buddha {
  background-image: url('../public/images/buddha.png');
  background-position: top;
  opacity: 0.1;
  z-index: -1;
  overflow: hidden;
  position: absolute;
  height: 100%;
  width: 200px;


}

</style>
