<template lang="html">
  <div>
    <li v-on:click="onClick">{{ beer.name }}</li>
  </div>
</template>

<script>
import{eventBus} from '../main.js';

export default {
  name: 'beer-list-item',
  props: ['beer'],
  methods: {
    onClick() {
      eventBus.$emit('selected-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
