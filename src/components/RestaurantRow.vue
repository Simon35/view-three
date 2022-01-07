<template>
  <div class="restaurant--row">
    <h2 class="title">
      Nos restaurants
    </h2>
    
    <div class="wrapper--card">
      <RestaurantCard v-for="(card, index) in three_restau" :info_restau="card" :key="index" />
    </div>
  </div>
</template>

<script>
import RestaurantCard from './RestaurantCard.vue'
export default {
  name: "RestaurantRow",
  components: {
    RestaurantCard
  },
  props: {
    three_restau: Array
  }
}
</script>

<style lang='scss'>
.restaurant--row {
  .title {
    font-size:2rem;
  }
  .wrapper--card {
    display:flex;
    align-items: center; //aligner les elts enfants ici name et note
    justify-content: space-between; // repoousse aux extremités jcsb

  }
}
</style>