<template>
  <div>
    <AppHeader />
    <div class="hero">
      <div class="hero-container">
        <div class="hero-text-con">
          <div class="hero-text-con-heading">
            <h1>Find recipes for the ingredients you have on hand</h1>
            <button @click="$router.push({ name: 'Search' })">
              Search Now
            </button>
          </div>
        </div>
        <div class="hero-image-con">
          <img src="../assets/plate3.png" alt="" />
          <div class="bar"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import AppHeader from "@/components/AppHeader.vue";

export default {
  name: "HomeView",
  components: {
    AppHeader,
  },
};
</script>

<style lang="scss" scoped>
@import "@/scss/Home.scss";
</style>