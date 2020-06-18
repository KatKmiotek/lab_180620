<template lang="html">
  <div>
    <p>Your Favourite Beers</p>
  <li v-for= "(beer, index) in favouriteBeers" :beer="beer" :key="index" :value="beer">
    {{beer.name}}<button type="button"v-on:click="removeFromFavourites">Remove</button>
  </li>
</div>
</template>

<script>
import {eventBus} from '../main.js'

export default {
  name: 'favourite-beers',
  props: ['favouriteBeers'],
  methods:{
    removeFromFavourites(){
      eventBus.$emit('remove-favourite', this.beer)
    }
  }

}
</script>

<style lang="css" scoped>
</style>
