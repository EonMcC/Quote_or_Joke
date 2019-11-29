<template>
  <div id="app">
    <h1>Quote or Joke?</h1>
    <quote-box :quoteBox="currentQuote"></quote-box>

  </div>
</template>

<script>
import {eventBus} from './main.js';
import QuoteBox from './components/QuoteBox.vue';
import QuoteItem from './components/QuoteItem.vue';

export default {
  name: 'app',
  data(){
    return {
      quotes: [],
      jokes:[],
      currentQuote: null
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
  .then(joke => this.jokes.push(joke))
},
components: {
  "quote-box": QuoteBox,
  "quote-item": QuoteItem
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
