<script setup>
import { defineProps } from 'vue';

const { data } = defineProps({
    data: Array
})
</script>

<!-- из пропа data выводим данные определённого рецепта -->

<template>
    <div class="recipeList">
        <div v-for="info in data">
            <div class="recipe">
                <img :src=info.image alt="#">
                <div class="recipeMain">
                    <div class="mainInfo">
                        <h2>{{ info.name }}</h2>
                        <p>Difficulty: {{ info.difficulty }}</p>
                        <p>Cuisine: {{ info.cuisine }}</p>
                        <p>Calories per Serving: {{ info.caloriesPerServing }}</p>
                    </div>
                    <div class="ingredients">
                        <h3>Ingredient:</h3>
                        <ul v-for="elem in info.ingredients">
                            <li>{{ elem }}</li>
                        </ul>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
img {
    width: inherit;
    border-top-right-radius: 25px;
    border-top-left-radius: 25px;
}

.recipeList {
    margin-top: 53px;
    display: flex;
    column-gap: 30px;
    row-gap: 60px;
    flex-wrap: wrap;
    justify-content: space-between;
}

.recipe {
    border-radius: 25px;
    background-color: #FFF;
    box-shadow: 0px 4px 4px 0px #00000040;
    width: 270px;
}

.recipeMain {
    padding: 12px 12px 32px 12px;
}

ul {
    line-height: 14.52px;
}

@media screen and (max-width: 700px) {
    .recipeList {
        justify-content: center;
    }
}
</style>