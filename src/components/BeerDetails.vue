<template lang="html">
  <div class="beer-details" v-if="beer">
    <h3>Name: {{ beer.name }}</h3>
    <img :src="beer.image_url" alt="beer-label" height="200">
    <p>abv: {{beer.abv}}</p>
    <p>Tag line: {{beer.tagline}}</p>
    <p>Goes with: {{ beer.food_pairing[0]}} or {{beer.food_pairing[1]}}</p>
    <ul v-for="(ingredient,index) in beer.ingredients">
      <li>{{ingredient.name}}</li>
    </ul>
  </div>
</template>

<script>

export default {
  name: 'beer-details',
  props: ['beer'],

}
</script>

<style lang="css" scoped>
.beer-details{
  border: solid 2px black;
  box-sizing: border-box;
  text-align: center;
}
</style>
