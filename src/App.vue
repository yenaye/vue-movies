<script setup>
import MovieHeader from './components/MovieHeader.vue';
import MovieList from './components/MovieList.vue';
import MovieFooter from './components/MovieFooter.vue';
import { ref, onMounted } from 'vue';
import { initFlowbite } from 'flowbite';

const movies = ref([]); // 영화 정보 결과 값
const options = {
    method: 'GET',
    headers: {
        accept: 'application/json',
        Authorization: 'Bearer {Authorization Key}'
    }
}; // 영화 API 옵션 걊
let menuIndex = 0; // 메뉴 Index

// 영화 API 제목 검색 이벤트
function searchEventHandler(event) {
    if (event == '') {
        menuEventHandler(menuIndex); // 영화 API 메뉴 이벤트
    } else {
        fetch('https://api.themoviedb.org/3/search/movie?query=' + event + '&include_adult=false&language=ko&page=1&region=kr', options)
            .then(response => response.json())
            .then(response => movies.value = response.results)
            .catch(err => console.error(err));
    }
}

// 영화 API 메뉴 이벤트
function menuEventHandler(event) {
    let apiType = ''; // API 타입
    switch (event) {
    case 0:
        apiType = 'now_playing'; // API 타입(현재 상영중)
        break;
    case 1:
        apiType = 'popular'; // API 타입(인기 상영작)
        break;
    case 2:
        apiType = 'top_rated'; // API 타입(높은 평점)
        break;
    }
    fetch('https://api.themoviedb.org/3/movie/' + apiType + '?language=ko&page=1&region=kr', options)
        .then(response => response.json())
        .then(response => movies.value = response.results)
        .catch(err => console.error(err));
    
    menuIndex = event; // 메뉴 Index
}

onMounted(() => {
    initFlowbite();
    menuEventHandler(menuIndex); // 영화 API 메뉴 이벤트
})
</script>

<template>
    <movie-header @searchTextInput="searchEventHandler" @menuIndex="menuEventHandler"></movie-header>
    <movie-list :movies="movies"></movie-list>
    <movie-footer></movie-footer>
</template>

<style scoped>
</style>