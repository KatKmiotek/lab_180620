<template lang="html">
<ul>
<beer-item v-for= "(beer, index) in beers" :beer= 'beer' :key='index'></beer-item>
</ul>
</template>

<script>
import BeerItem from './BeerItem.vue'

export default {
  name: 'beers-list',
  props: ['beers'],
  components: {
    'beer-item': BeerItem
  }
}
</script>

<style lang="css" scoped>
</style>
