<template>
  <div>
      <header class="beer-header">
        <hgroup>
          <h2>{{ beer.name }}</h2>
          <h4>{{beer.tagline}}</h4>
        </hgroup>
        <button @click="handleClick">Add to Favourites</button>
      </header>
      <p>{{ beer.description }}</p>
      <div class="beer-stats">
        <img :src="beer.image_url" :alt="beer.name">
        <aside class="stat-text">
          <p>First brewed: {{ beer.first_brewed }}</p>
          <p>ABV: {{ beer.abv }}%</p>
          <p>Ingredients: {{ getIngredients(beer) }}</p>
        </aside>
      </div>
  </div>
</template>

<script>
import { eventBus } from '../main.js'

export default {
  name: "beer-detail",
  props: ['beer'],
  methods: {
    handleClick() {
      eventBus.$emit("favourite-beer", this.beer)
    },
    getIngredients(beer) {
      const ingredients = []
      beer.ingredients.malt.forEach(malt => ingredients.push(malt.name))
      beer.ingredients.hops.forEach(hop => ingredients.push(hop.name))
      ingredients.push(beer.ingredients.yeast)

      let uniqueIngredients = ingredients.filter((ingredient, index) => ingredients.indexOf(ingredient) === index)

      return uniqueIngredients.join(', ')
    }

  }
}
</script>

<style scoped>

div > img {
  width:10%;
}

.beer-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.beer-stats {
  display: flex;
  align-items: center;
  margin: 20px;
}

.stat-text {
  padding: 20px;
}

</style>