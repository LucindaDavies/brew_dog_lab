<template>
  <div>
    <h1>BrewDog Beers</h1>
    <div class="drop-down-container">
      <beer-select :beers="beers"></beer-select>
    </div>
    <beer-detail v-if="selectedBeer" :beer="selectedBeer"></beer-detail>
    <favourite-beers v-if="favouriteBeers.length > 0" :beers="favouriteBeers"></favourite-beers>
  </div>

</template>

<script>
import BeerSelect from './components/BeerSelector.vue'
import BeerDetail from './components/BeerDetail.vue'
import FavouriteBeers from './components/FavouriteBeers.vue'
import { eventBus } from './main.js'

export default {
  name: 'app',
  data(){
    return {
      beers: [],
      selectedBeer: null,
      favouriteBeers: []
    }
  },
  mounted() {
    fetch('https://api.punkapi.com/v2/beers?per_page=80')
    .then(res => res.json())
    .then(beers => this.beers = beers)

    eventBus.$on("beer-selected", (beer) => this.selectedBeer = beer)
    eventBus.$on("favourite-beer", (beer) => {
      if (!this.favouriteBeers.includes(beer)) {
        this.favouriteBeers.push(beer)
        };
      })
    eventBus.$on("remove-beer", (beer) => {
      let favourites= this.favouriteBeers.filter((favourite) => favourite !== beer)
      this.favouriteBeers = favourites
    })
  },
  components: {
    "beer-select": BeerSelect,
    "beer-detail": BeerDetail,
    "favourite-beers": FavouriteBeers
  }
}
</script>

<style>

</style>
