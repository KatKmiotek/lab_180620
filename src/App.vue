<template lang="html">
  <div>
  <nav>
  <h1>Brewdog App</h1>
</nav>
  <favourite-beers :favouriteBeers = 'favouriteBeers'>Your Favourites</favourite-beers>
  <beer-details :beer = 'selectedBeer'></beer-details>
  <beers-list :beers = 'beers'>Beers</beers-list>
</div>
</template>

<script>
import { eventBus } from './main.js'
import BeersList from './components/BeersList.vue'
import BeerDetails from './components/BeerDetails.vue'
import FavouriteBeers from './components/FavouriteBeers.vue'

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  computed: {

  },
  mounted() {
    const pageOne = fetch("https://api.punkapi.com/v2/beers?page=1&per_page=80");
    const pageTwo = fetch("https://api.punkapi.com/v2/beers?page=2&per_page=80");
    const pageThree = fetch("https://api.punkapi.com/v2/beers?page=3&per_page=80");
    const pageFour = fetch("https://api.punkapi.com/v2/beers?page=4&per_page=80");
    const pageFive = fetch("https://api.punkapi.com/v2/beers?page=5&per_page=80");
    Promise.all([pageOne, pageTwo, pageThree, pageFour, pageFive])
      .then((responses) => Promise.all(responses.map(response => response.json())))
      .then(data => this.beers = data.flat())

    eventBus.$on('selected-beer', (beer) => {
      this.selectedBeer = beer
    })

    eventBus.$on('favourite-beer', (beer) => {
      if(!this.favouriteBeers.includes(beer)){
      this.favouriteBeers.push(beer)}
    })

    eventBus.$on('remove-favourite', (beer) => {
      this.favouriteBeers.pop(beer)
    })
  },
  components: {
    'beers-list': BeersList,
    'beer-details': BeerDetails,
    'favourite-beers': FavouriteBeers
  }
}
</script>

<style lang="css" scoped>
nav {
text-align: center;
}
beer-list {
  display: flex;
  flex-direction: column;
}
</style>
