<template lang="html">
  <div>
  <nav>
  <h1>Brewdog App</h1>
  <button type="button" name="button">Discover Beers</button>
  <button type="button" name="button" v-on:click="seeFavourtites">Favourites</button>
</nav>
  <beer-details :beer = 'selectedBeer'></beer-details>
  <beers-list :beers = 'beers'></beers-list>
</div>
</template>

<script>
import { eventBus } from './main.js'
import BeersList from './components/BeersList.vue'
import BeerDetails from './components/BeerDetails.vue'

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null
    }
  },
  computed: {
    seeFavourtites(){
      return this.beers.filter((beer) => {
        return beer.favouriteBeer == true
      })
    }
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers')
    .then(response => response.json())
    .then(data => this.beers = data)

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer
    })
  },
  components: {
    'beers-list': BeersList,
    'beer-details': BeerDetails
  }
}
</script>

<style lang="css" scoped>
nav {
text-align: center;
}
</style>
