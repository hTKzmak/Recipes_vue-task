<script setup>

import { ref, reactive } from 'vue';
import Menu from './components/Menu.vue'
import Recipes from './components/Recipes.vue'

let data = reactive([]);

fetch('https://dummyjson.com/recipes')
  .then(res => res.json())
  .then(json => {
    data.push(...json.recipes.map(elem => elem));
  });

let currentPage = ref(1);
let itemsPerPage = 6;
let totalItems = data.length;

let menuListarr = [];
for (let i = 1; i < itemsPerPage; i++) {
  menuListarr.push(i)
}

function nextPage() {
  if (menuListarr.length != currentPage.value) {
    currentPage.value++
    goToPage(currentPage.value)
  }
}

function previousPage() {
  if (menuListarr[0] != currentPage.value) {
    currentPage.value = currentPage.value - 1
    goToPage(currentPage.value)
  }
}

function totalPages() {
  return Math.ceil(totalItems / itemsPerPage);
}

function goToPage(pageNumber) {
  currentPage.value = pageNumber;
}

function getVisibleRecipes() {
  const startIndex = (currentPage.value - 1) * itemsPerPage;
  const endIndex = startIndex + itemsPerPage;
  return data.slice(startIndex, endIndex);
}

</script>

<template>
  <header class="title">
    <h1>Recipes</h1>
  </header>
  <main>
    <div class="container">
      <Menu :totalPages="totalPages" :goToPage="goToPage" :currentPage="currentPage" :nextPage="nextPage"
        :previousPage="previousPage" :itemsPerPage="itemsPerPage" :menuListarr="menuListarr" />
      <Recipes :data="getVisibleRecipes()" />
    </div>
  </main>
</template>

<style>
.title {
  text-align: center;
}
</style>
