<template lang="html">
  <div>
    <h1>No they didn't!</h1>
    <button type="button" v-on:click="handleClickCombo">Generate</button>
    <p v-if="comboJoke">{{comboJoke}}</p>
    <h3 v-if="comboQuote">~{{comboQuote}}~</h3>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
  name: "combo-box",
  props: ['comboJoke', 'comboQuote'],
  methods: {
    handleClickCombo(){
      eventBus.$emit('loadCombo');
    }
  }
}

</script>

<style lang="css" scoped>
</style>
