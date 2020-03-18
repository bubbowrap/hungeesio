<template>
  <div id="app">
    <div class="container">
      <div class="row justify-content-sm-center">
        <div class="col-sm-8">
          <h1>Hungees.io</h1>
          <p>Serving up (ugh) meal ideas based on what you already have.</p>
        </div>
      </div>
      <div class="row justify-content-sm-center">
        <div class="col-sm-8 mb-3">
          <recipe-search></recipe-search>
        </div>
      </div>
      <div class="row justify-content-sm-center">
        <div class="col-sm-12 mb-3">
          <recipe-grid></recipe-grid>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import RecipeSearch from './components/RecipeSearch.vue';
import RecipeGrid from './components/RecipeGrid.vue';

export default {
  name: "App",
  components: {
    RecipeSearch,
    RecipeGrid
  }
};
</script>

<style lang="scss">
body {
    background-color: #F1F1F1;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
