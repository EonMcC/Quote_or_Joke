<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>No they didn't!</h3>
    <hr>
    <p v-show="display" :joke="joke" v-if="comboJoke">{{comboJoke}}</p>
    <h3 v-show="display" :joke="joke" v-if="comboQuote">~{{comboQuote}}~</h3>
    <button v-show="display" :joke="joke" type="button" v-on:click="handleClickCombo">Generate</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: "combo-box",
  data(){
    return {
      display: false
    };
  },
  props: ['comboJoke', 'comboQuote'],
  methods: {
    handleClickCombo(){
      eventBus.$emit('loadCombo');
    },
    mouseOver: function(){
    this.display = !this.display;
      }
  }
}

</script>

<style lang="css" scoped>
</style>
