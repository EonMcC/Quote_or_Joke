<template>
  <div id="app">
    <h1>Quote or Joke?</h1>
    <quote-box :quoteBox="currentQuote"></quote-box>
    <fave-quote-box :faveQuotes="faveQuotes"></fave-quote-box>
    <joke-box :joke="currentJoke"></joke-box>
    <fave-joke-box :faveJokes="faveJokes"></fave-joke-box>
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




export default {
  name: 'app',
  data(){
    return {
      quotes: [],
      jokes:[],
      currentQuote: null,
      faveQuotes: [],
      currentJoke: null,
      faveJokes: []
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
},
components: {
  "quote-box": QuoteBox,
  "quote-item": QuoteItem,
  "fave-quote-box": FaveQuoteBox,
  "fave-quote-detail": FaveQuoteDetail,
  "joke-box": JokeBox,
  "fave-joke-box": FaveJokeBox,
  "fave-joke-detail": FaveJokeDetail
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
  margin-top: 60px;
}
</style>
