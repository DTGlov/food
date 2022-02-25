<template>
  <div class="search-wrapper">
    <AppHeader />
    <div class="search">
      <div class="search-area">
        <p>What ingredients do you have?</p>
        <form @submit.prevent="searchFood" action="">
          <div class="form-wrapper">
            <i class="fas fa-search fa-lg"></i>
            <input type="text" placeholder="" v-model="term" />
          </div>
        </form>
      </div>
      <div class="icon-img">
        <img src="../assets/search-icons.png" alt="" />
      </div>
    </div>
    <div class="food-heading" v-if="!term">
      <h1>Food will appear here!</h1>
    </div>
    <div class="card-wrapper" v-if="menuItems">
      <!-- <div
        class="card"
        v-for="meal in menuItems.slice(0, 10)"
        :key="meal.idMeal"
      >
        <div class="card-img-container">
          <img :src="meal.strMealThumb" alt="" />
        </div>
        <p class="card-text">{{ meal.strMeal }}</p>
      </div> -->
      <FoodCard
        v-for="meal in menuItems.slice(0, 10)"
        :meal="meal"
        :key="meal.idMeal"
      />
    </div>
    <div class="skeleton-wrapper" v-if="term.length > 0 && !menuItems">
      <div>
        <div class="skeleton-wrapper-card"></div>
        <div class="small-bar"></div>
      </div>
      <div>
        <div class="skeleton-wrapper-card"></div>
        <div class="small-bar"></div>
      </div>
      <div>
        <div class="skeleton-wrapper-card"></div>
        <div class="small-bar"></div>
      </div>
      <div>
        <div class="skeleton-wrapper-card"></div>
        <div class="small-bar"></div>
      </div>
    </div>
    <!-- <div v-else>
      <p>Food not Found</p>
    </div> -->
  </div>
</template>

<script>
import AppHeader from "@/components/AppHeader.vue";
import MenuService from "@/services/MealServices.js";
import FoodCard from "@/components/FoodCard.vue";

export default {
  name: "SearchView",
  components: { AppHeader, FoodCard },
  data() {
    return {
      menuItems: null,
      term: "",
    };
  },
  watch: {
    // whenever term changes, this function will run
    term(newTerm, oldTerm) {
      if (newTerm.length > 0) {
        this.searchFood();
      }
    },
  },
  methods: {
    searchFood() {
      MenuService.getMenu(this.term).then((response) => {
        this.menuItems = response.data.meals;
        console.log(response.data);
        console.log("menu", this.menuItems);
      });
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/Search.scss";
</style>