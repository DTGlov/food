<template>
  <header>
    <nav class="nav">
      <div class="nav-image-container">
        <img src="../assets/food-logo.png" alt="" />
      </div>
      <ul class="nav-link">
        <li class="nav-link-item">
          <router-link :to="{ name: 'home' }">Home</router-link>
        </li>

        <li class="nav-link-item">
          <router-link :to="{ name: 'Search' }">Search</router-link>
        </li>
      </ul>
    </nav>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
};
</script>

<style lang="scss" scoped>
@import "@/scss/AppHeader.scss";
</style>