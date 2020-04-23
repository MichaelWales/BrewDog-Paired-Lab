<template lang="html">
  <div>
    <h1>🍻 BrewDog Beers 🍻</h1>
    <beer-list :beers="beers"></beer-list>
    <beer-detail v-if="selectedBeer" :beer="selectedBeer"></beer-detail>
    <beer-favourites v-if="favouriteBeers" :favouriteBeers="favouriteBeers"></beer-favourites>
  </div>
</template>

<script>
import BeerList from './components/BeerList.vue';
import {eventBus} from './main.js';
import BeerListItem from './components/BeerListItem.vue';
import BeerDetail from './components/BeerDetail.vue';
import BeerFavourites from './components/BeerFavourites.vue';

export default {
  name: 'app',
  data() {
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  mounted(){
    fetch('https://api.punkapi.com/v2/beers')
    .then(response => response.json())
    .then(beers => this.beers = beers)

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer;
    }),

    eventBus.$on('favourite-beer', (beer) => {
      if (this.favouriteBeers.includes(beer)){
        alert("No Double-Dipping! Pick another beer!")
      }else{
      this.favouriteBeers.push(beer);
    }}),

    eventBus.$on('delete-beer', (beer) => {
      const index = this.favouriteBeers.indexOf(beer)
      this.favouriteBeers.splice(index, 1)
    })

  },

  components: {
    'beer-list': BeerList,
    'beer-list-item': BeerListItem,
    'beer-detail': BeerDetail,
    'beer-favourites': BeerFavourites
  }
}
</script>

<style lang="css" scoped>
</style>
