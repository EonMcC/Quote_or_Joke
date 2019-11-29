<template lang="html">
  <div>
    <joke-item :joke="joke"></joke-item>
  </div>
</template>

<script>
import JokeItem from './JokeItem.vue';
export default {
  name: "joke-box",
  props: ['joke'],
  components: {
    "joke-item": JokeItem
  }
}
</script>

<style lang="css" scoped>
</style>
