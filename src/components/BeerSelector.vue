<template>
    <select name="beer-select" id="beer-select" @change="handleChange" v-model="selectedBeer">
      <option disabled selected>Select a Beer...</option>
      <option v-for="beer in beers" :value="beer" :key="beer.id"> {{ beer.name }} </option>
    </select>
</template>

<script>

import { eventBus } from '../main.js'
export default {
    name: "beer-select",
    props: ['beers'],
    data() {
        return {
            selectedBeer: null
        }
    },
    methods: {
        handleChange() {
            eventBus.$emit("beer-selected", this.selectedBeer)
        }
    }
}
</script>

<style>

</style>