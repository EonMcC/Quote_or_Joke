<template lang="html">
  <div @mouseover="mouseOver" @mouseout="mouseOver">
    <hr>
    <h3>Joke</h3>
    <hr>
    <joke-item v-show="display" :joke="joke"></joke-item>
    <button v-show="display" :joke="joke" type="button" v-on:click="handleClickJokeReload">Try Again!</button>
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
        }
  }
}
</script>

<style lang="css" scoped>
</style>
