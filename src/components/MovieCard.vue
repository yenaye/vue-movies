<script setup>
const props = defineProps(['movie']); // 영화 정보
const imageUrl = 'https://image.tmdb.org/t/p/w500' + props.movie.poster_path; // 이미지 URL
</script>

<template>
    <div class="m-3 max-w-sm bg-white border border-gray-200 rounded-lg shadow dark:bg-gray-800 dark:border-gray-700">
        <a href="#">
            <img class="rounded-t-lg" :src="imageUrl" alt="" />
        </a>
        <div class="p-5">
            <a href="#">
                <h5 class="mb-2 text-2xl font-bold tracking-tight text-gray-900 dark:text-white">
                    {{ movie.title }}
                </h5>
            </a>
            <p class="mb-3 font-normal text-gray-700 dark:text-gray-400">
                {{ movie.overview }}
            </p>
        </div>
    </div>
</template>

<style scoped>
</style>