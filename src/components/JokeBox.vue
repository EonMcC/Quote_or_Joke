<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Joke</h3>
    <hr>
    <transition name="fade">
      <div v-show="display">
        <joke-item :joke="joke"></joke-item>
        <button :joke="joke" type="button" v-on:click="handleClickJokeReload">Try Again!</button>
      </div>
    </transition>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import JokeItem from './JokeItem.vue';
export default {
  name: "joke-box",
  data(){
    return {
      display: false
    };
  },
  props: ['joke'],
  components: {
    "joke-item": JokeItem
  },
  methods: {
    handleClickJokeReload(){
      eventBus.$emit('reloadJoke');
    },
    mouseOver: function(){
      this.display = !this.display;
      eventBus.$emit('faveJokeDisplay', this.display);
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
