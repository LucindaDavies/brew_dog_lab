<template>
  <div id="favourites">
    <header>
      <h2>Favourite Beers</h2>
    </header>
    <favourite-beer v-for="beer in beers" :key="beer.id" :beer="beer"></favourite-beer>
  </div>
</template>

<script>
import FavouriteBeer from './FavouriteBeer.vue'

export default {
    name: "favourite-beers",
    props: ["beers"],
    components: {
      "favourite-beer": FavouriteBeer
    }
  }

</script>

<style scoped>

</style>