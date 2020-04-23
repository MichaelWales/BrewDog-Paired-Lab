<template lang="html">
  <div>
    <h3>{{beer.name}}</h3>
    <button v-on:click="onClick" name="Add to Favourites">Add to Favourites</button>
    <img width="50px" :src="beer.image_url">
    <h4>Description:</h4>
    <p>{{beer.description}}</p>
    <br>
    <h4>Brewer's Tips:</h4>
    <p>{{beer.brewers_tips}}</p>
    <br>
    <h4>Food Pairings:</h4>
    <p v-for="(pairing, index) in beer.food_pairing">{{pairing}}</p>
  </div>
</template>

<script>
import {eventBus} from '../main.js';

export default {
  name: 'beer-detail',
  props: ['beer'],
  methods: {
    onClick() {
      eventBus.$emit('favourite-beer', this.beer)
    },
    showIngredients() {
      const ingredients = []
      return this.beer.ingredients.map(item => {
        
      })
    }
  }
}
</script>

<style lang="css" scoped>
</style>
