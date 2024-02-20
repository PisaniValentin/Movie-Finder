<script setup lang="ts">
import axios from 'axios';
import { watch, ref } from 'vue'

type movie = {
    cast: string,
    country: string,
    date_added: Date,
    title: string,
    director: string,
    duration: string,
    description: string
}

defineProps({
    movies: String
})

const search = ref('')
let moviesList = ref<Array<movie>>([]);

async function getData() {
    await axios.get(`http://localhost:8080/api/suggestTitle/${search.value}`)
        .then((response) => {
            console.log(response.data)
            moviesList.value = response.data;
        })
        .catch((error) => {
            console.log(error)
        })
}

watch(search, () => {
    if (search.value != '') {
        getData()
    }
})
</script>

<template>
    <input v-model="search" class="p-1 w-1/3 self-center" type="text" placeholder="Enter a movie title..">
    <main class="flex flex-col overflow-scroll overflow-x-hidden h-4/5 w-1/2 pt-3">
        <section class="text-white/80" v-for="movie in moviesList" :key="movie.title">
            <h2 class=" text-2xl text-red-500/80">{{ movie.title }}</h2>
            <p>{{ movie.description }}</p>
            <p>Duration: {{ movie.duration }}</p>
            <p v-if="movie.director">Director: {{ movie.director }}</p>
        </section>
    </main>
</template>