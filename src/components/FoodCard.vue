<template>
  <router-link :to="{ name: 'FoodDetails', params: { id: meal.idMeal } }">
    <div class="card">
      <div class="card-img-container">
        <img :src="meal.strMealThumb" alt="" />
      </div>
      <p class="card-text">{{ meal.strMeal }}</p>
    </div>
  </router-link>
</template>

<script>
export default {
  name: "FoodCard",
  props: ["meal"],
};
</script>

<style lang="scss" scoped>
@import "@/scss/Search.scss";
</style>