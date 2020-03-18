<template>
    <div class="input-group input-group-lg mb-3">
    <input type="text" :class="['form-control', {'is-invalid' : error}]" @keyup.enter="fetchRecipes" placeholder="insert an ingredient..." v-model="ingredient">
    <div class="input-group-append">
      <button class="btn btn-danger font-weight-bold" type="button" @click="fetchRecipes">Get Meal Ideas</button>
    </div>
        <div class="invalid-feedback text-left">Invalid entry. Please try again.</div>

</div>
</template>

<script>
import axios from 'axios';
import { EventBus } from './../main';

export default {
    data() {
        return {
            ingredient: '',
            error: false,
            meals: []
        }
    },
    methods : {
        fetchRecipes() {
            const endpoint = 'https://www.themealdb.com/api/json/v1/1/filter.php';
            let formattedIngredient = this.ingredient.trim().replace(/\s/g, '_');
            let mealLimit = 12;

            if (formattedIngredient) {
                EventBus.$emit('pushIngredient', this.ingredient);

                axios.get(`${endpoint}?i=${formattedIngredient}`)
                    .then(res => {
                        if (res.data.meals === null) {
                            this.error = true;
                            EventBus.$emit('updateError', this.error);
                            this.ingredient = '';
                        } else {
                        this.meals = [...res.data.meals].splice(0, mealLimit);
                        EventBus.$emit('pushRecipe', this.meals);
                        }

                    })
                    .catch(err => {
                        console.log(err);
                });
            } else {
                this.error = true;
            }
        }
    }
}
</script>