<template lang="html">
  <div>
    <h3>Favourites</h3>
    <ul>
      <li v-for="(beer, index) in favouriteBeers" :beer="beer" :key="index">
        <button v-on:click="onClick(beer)">Delete {{beer.name}}</button>
        <img width="25px" :src="beer.image_url">
      </li>
    </ul>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-favourites',
  props: ['favouriteBeers'],
  methods: {
    onClick(beer){
      eventBus.$emit('delete-beer', beer)
    }
  }
}
</script>

<style lang="css" scoped>
</style>
