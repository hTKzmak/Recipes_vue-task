<script setup>
import { defineProps } from 'vue';

const { totalPages, goToPage, currentPage, nextPage, previousPage, itemsPerPage, menuListarr } = defineProps({
    totalPages: Function,
    goToPage: Function,
    currentPage: Number,
    nextPage: Function,
    previousPage: Function,
    itemsPerPage: Number,
    menuListarr: Number
})

// просто знаки
let left_sign = '<';
let right_sign = '>';

</script>

<template>
    <div class="list">
        <button @click="previousPage">{{ left_sign }}</button>
        <div class="listNum">
            <button v-for="pageNumber in menuListarr" @click="goToPage(pageNumber)" :class="[currentPage == pageNumber ? 'activePage' : '']">
                {{ pageNumber }}
            </button>
        </div>
        <button @click="nextPage">{{ right_sign }}</button>
    </div>
</template>


<style>
.list {
    display: flex;
    justify-content: center;
    gap: 20px;
}

.listNum {
    display: flex;
    gap: 20px;
}

.activePage{
    border: 1px solid #185bc3;
    background-color: #185bc3;
    color: #fff;
}

.activePage:hover{
    border: 1px solid #0167ff;
    background-color: #0066ff;
    color: #fff;
}

button {
    border: 1px solid #BDBDBD;
    padding: 26px 28px;
    font-size: 18px;
    font-weight: 800;
    color: #BDBDBD;
    background: none;
    border-radius: 6px;
}

button:hover {
    background: #c9c9c93b;
}

.active {
    border: 1px solid #185BC3;
    color: #FFF;
    background: #185BC3;
}
</style>