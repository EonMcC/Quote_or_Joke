<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>No they didn't!</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <p v-if="comboJoke">{{comboJoke}}</p>
        <h3 v-if="comboQuote">~{{comboQuote}}~</h3>
        <button v-show="display" type="button" v-on:click="handleClickCombo">Generate</button>
      </div>
    </transition>
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
  .fade-enter-active, .fade-leave-active {
    transition: opacity 1s;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  button {
    margin: 10px;
  }
</style>
