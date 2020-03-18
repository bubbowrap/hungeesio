<template>
  <div class="container">
    <div class="row text-center mb-4" v-if="ingredient">
      <div class="col-sm-12">
        <h2>Returned {{recipeData.length}} results for '{{ingredient}}'</h2>
      </div>
    </div>
      <div class="row">
        <recipe-block v-for="(recipe,index) in recipeData" :key="index" :recipe="recipe"></recipe-block>
      </div>
  </div>
</template>

<script>

import RecipeBlock from './RecipeBlock.vue';

import { EventBus } from './../main';

export default {
    data() {
        return {
            recipeData: [],
            ingredient: '',
            error: false
        }
    },
    components: {
      RecipeBlock
    },
    methods: {
      updateRecipes() {
        if (this.error) {
          this.recipeData = [];
        }         
      }
    },
    created() {
        EventBus.$on('updateError', data => {
            this.error = data;
            this.updateRecipes();
          });

        EventBus.$on('pushIngredient', data => {
          this.ingredient = data;
        });

        EventBus.$on('pushRecipe', data => {
            this.recipeData = [...data];
        });
    }
}
</script>