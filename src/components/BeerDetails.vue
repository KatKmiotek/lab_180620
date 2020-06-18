<template lang="html">
  <div class="beer-details" v-if="beer">
    <h3>Name: {{ beer.name }}</h3>
    <img :src="beer.image_url" alt="beer-label" height="200">
    <p>abv: {{beer.abv}}</p>
    <p>Tag line: {{beer.tagline}}</p>
    <p>Goes with: {{ beer.food_pairing[0]}} or {{beer.food_pairing[1]}}</p>
    <button type="button" v-on:click="addToFavourites" v-if='!favouriteBeer'>Add to favourites</button>
  </div>
</template>

<script>

export default {
  name: 'beer-details',
  data(){
    return {
      favouriteBeer: false
    }
  },
  props: ['beer'],
methods: {
  addToFavourites(){
    this.favouriteBeer= true
  }
  }
}
</script>

<style lang="css" scoped>
.beer-details{
  border: solid 2px black;
  box-sizing: border-box;
  text-align: center;
}
</style>
