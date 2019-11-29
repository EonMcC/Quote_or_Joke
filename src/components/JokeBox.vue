<template lang="html">
  <div>
    <joke-item :joke="joke"></joke-item>
    <button type="button" v-on:click="handleClickJokeReload">Try Again!</button>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
import JokeItem from './JokeItem.vue';
export default {
  name: "joke-box",
  props: ['joke'],
  components: {
    "joke-item": JokeItem
  },
  methods: {
    handleClickJokeReload(){
      eventBus.$emit('reloadJoke');
    }
  }
}
</script>

<style lang="css" scoped>
</style>
