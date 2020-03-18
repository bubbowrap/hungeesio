<template>
    <div class="col-md-4 mb-5">
        <img :src="recipe.strMealThumb" alt="recipe.strMeal">
        <h4 class="mt-2">{{recipe.strMeal}}</h4>
    </div>
</template>

<script>
    export default {
        props: ['recipe']
    }

</script>

<style>
    img {
        max-width: 100%;
    }
</style>