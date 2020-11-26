<template>
  <div class="favourite-box">
      <div>
        <img :src="beer.image_url" class="beer-icon">
      </div>
      <h3>{{ beer.name }}</h3>
      <button @click="handleClick">Remove</button>
  </div>
</template>

<script>
import { eventBus } from '../main.js';

export default {
    name: "favourite-beer",
    props: ['beer'],
    methods: {
    handleClick() {
      eventBus.$emit("remove-beer", this.beer)
      },
    }
}

</script>

<style scoped>
.beer-icon {
  height: 100px;
  width: auto;
  padding: 20px;
  margin: 10px;
}

.favourite-box {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  margin: 5px;
  padding: 0px 10px;
  border: 1px solid grey;
  border-radius: 10px;
}

</style>