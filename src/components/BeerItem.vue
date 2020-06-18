<template lang="html">
<li>{{beer.name}}
<button type="button" v-on:click= 'handleClick'>Details</button>
<button type="button" v-on:click= 'addToFavourites'>Add to favourites</button>
</li>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: 'beer-item',
  props: ['beer'],
  methods: {
    handleClick() {
      eventBus.$emit('selected-beer', this.beer)
    },
    addToFavourites() {
      eventBus.$emit('favourite-beer', this.beer)
    }
  }
}
</script>

<style lang="css" scoped>
li{
  display: flex;
  flex-direction: row;
  justify-content: flex-start;
}

</style>
