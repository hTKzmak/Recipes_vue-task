<script setup>

import { ref, reactive } from 'vue';
import Menu from './components/Menu.vue'
import Recipes from './components/Recipes.vue'

// сами данные
let data = reactive([]);

// получаем данные
fetch('https://dummyjson.com/recipes')
  .then(res => res.json())
  .then(json => {
    data.push(...json.recipes.map(elem => elem));
  });

// текущая страница
let currentPage = ref(1);

// кол-во нужных рецептов
let itemsPerPage = 6;

// длина всех данных
let totalItems = data.length;

// возращает итоговое кол-во страниц
let menuListarr = [];
for (let i = 1; i < itemsPerPage; i++) {
  menuListarr.push(i)
}

// перемещаемя на следующую страницу
function nextPage() {
  if (menuListarr.length != currentPage.value) {
    currentPage.value++
    goToPage(currentPage.value)
  }
}

// перемещаемя на предыдущую страницу
function previousPage() {
  if (menuListarr[0] != currentPage.value) {
    currentPage.value = currentPage.value - 1
    goToPage(currentPage.value)
  }
}

// хз :P
function totalPages() {
  return Math.ceil(totalItems / itemsPerPage);
}

// ф-ия для изменения значение curretnPage в виде числа
function goToPage(pageNumber) {
  currentPage.value = pageNumber;
}

// отображает данные в зависимости от: startIndex (сколько продуктов должно быть на странице, умножая на текущий номер страницы - 1) 
// и от endIndex (прибавляем значение startIndex на кол-во нужных объектов на странице)
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

      <!-- здесь отображаем данные и нужное кол-во рецептов (это всё вместе, то есть получаем обрезанное кол-во файлов в зависимости от номера страницы)-->
      <Recipes :data="getVisibleRecipes()" />
    </div>
  </main>
</template>

<style>
.title {
  text-align: center;
}
</style>
