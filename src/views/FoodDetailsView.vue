<template>
  <div class="all">
    <AppHeader />
    <div class="search">
      <div class="search-area"></div>
      <div class="icon-img">
        <img src="../assets/search-icons.png" alt="" />
      </div>
    </div>
    <div class="food-container" v-for="food in foods" :key="food.idMeal">
      <div class="food-image">
        <img :src="food.strMealThumb" alt="" />
      </div>
      <div class="food-details">
        <h2>{{ food.strMeal }}</h2>
        <div class="food-details-card">
          <div class="food-details-card-item">
            <div class="img-text">
              <img src="../assets/cat.svg" alt="" />
              <p>CATEGORY</p>
            </div>

            <p class="food-para">{{ food.strCategory }}</p>
          </div>
          <div class="food-details-card-item marg">
            <div class="img-text">
              <img src="../assets/area.svg" alt="" />
              <p>AREA</p>
            </div>

            <p class="food-para">{{ food.strArea }}</p>
          </div>
          <div class="food-details-card-item marg">
            <div class="img-text">
              <img src="../assets/tag.svg" alt="" />
              <p>TAGS</p>
            </div>

            <div v-if="food.strTags">
              <p class="food-para">{{ food.strTags }}</p>
            </div>
            <div v-else>
              <p class="food-para">No Tag</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <!-- <div v-for="(food, index) in foods" :key="index">
      <div class="ingredients">
        <p>{{ food.strIngredient1 }}</p>
        <p>{{ food.strMeasure1 }}</p>
      </div>
    </div> -->
    <div class="ingredients">
      <h1>Ingredients</h1>
      <div class="pill-container">
        <div
          class="pill-container-item"
          v-for="(item, index) in getMeasureIngredient"
          :key="index"
        >
          <p>{{ item.ingredient }}</p>
          <div>
            <p>{{ item.measurement }}</p>
          </div>
        </div>
      </div>
    </div>
    <div class="instructions">
      <h1>Instructions</h1>
      <div v-for="(word, index) in getInstructions" :key="index">
        <p>{{ word }}</p>
      </div>
    </div>
    <div>
      <!-- {{ getIngredient }}
      {{ getMeasure }} -->
      <!-- {{ getMeasureIngredient }} -->
    </div>
  </div>
</template>

<script>
import MealServices from "@/services/MealServices";
import AppHeader from "@/components/AppHeader.vue";
export default {
  name: "FoodDetails",
  props: ["id"],
  components: { AppHeader },
  data() {
    return {
      foods: null,
      instructions: null,
      allIngredients: [],
      allMeasures: [],
    };
  },
  created() {
    MealServices.getFoodById(this.id).then((response) => {
      this.foods = response.data.meals;

      // if (this.food) {
      this.getIngredient();
      this.getMeasure();
      console.log("zz", this.allIngredients);
      console.log("ll", this.allMeasures);
      // }
    });
  },
  computed: {
    getInstructions() {
      if (this.foods) {
        let inst = this.foods.map((food) => food.strInstructions);
        let neww = inst[0];
        return neww.split("\r\n");
      }
    },
    getMeasureIngredient() {
      if (this.foods) {
        let foodObject = [];
        for (let i = 0; i < this.allIngredients.length; i++) {
          // for (let j = 0; j < this.allMeasures.length; j++) {
          foodObject.push({
            ingredient: this.allIngredients[i],
            measurement: this.allMeasures[i],
          });
          // }
        }
        return foodObject;
      }
    },
  },
  methods: {
    getIngredient() {
      let ingredients = [];
      if (this.foods) {
        return this.foods.forEach((food) => {
          // console.log(food);
          // return Object.keys(food).includes("strIngredient");
          for (const [key, value] of Object.entries(food)) {
            // console.log(`${key}: ${value}`);
            if (key.includes("strIngredient")) {
              ingredients.push(value);
              // this.ingredients = ingredient;
              let rr = ingredients
                .filter(
                  (ingredient) => ingredient.length !== 0 && ingredient !== null
                )
                .map((item) => item);
              this.allIngredients = rr;
              // console.log("meee", this.ngredients);
              // console.log("rrr", this.allIngredients);
              // console.log("ingredient", value);
              // return value;
            }
          }
        });
      }
    },
    getMeasure() {
      let measures = [];
      if (this.foods) {
        return this.foods.forEach((food) => {
          // console.log(food);
          // return Object.keys(food).includes("strIngredient");
          for (const [key, value] of Object.entries(food)) {
            // console.log(`${key}: ${value}`);
            if (key.includes("strMeasure")) {
              // console.log("measure", value);
              measures.push(value);
              // this.measures = measure;
              let vv = measures
                .filter((measure) => measure.length !== 0 && measure !== null)
                .map((item) => item);
              // return value;
              this.allMeasures = vv;
              console.log("vvvv", this.allMeasures);
            }
          }
        });
      }
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/Search.scss";
@import "@/scss/foodDetails.scss";
</style>