<script setup>
import { ref } from "vue";
import axios from "axios";
import SiteModal from "../components/SiteModal.vue";

let modalId = ref(null);
let openModal = ref(false);
let trendingMovies = ref(null);

const props = defineProps({
  movieId: String,
});

const getData = async (url, params) => {
  try {
    return await axios.get(url, params);
  } catch (error) {
    console.log(error);
  }
};

const getMovies = async () => {
  const movie = (
    await getData("https://api.themoviedb.org/3/trending/movie/week", {
      params: {
        api_key: "c6b2390c3ab4bfbd0e064d952df483c9",
        append_to_response: "videos",
      },
    })
  ).data.results;
  console.log(movie);
  if (trendingMovies.value == null) {
    trendingMovies.value = movie;
  } else {
    trendingMovies.value = trendingMovies.value(movie);
  }
  console.log(trendingMovies);
};
getMovies();

const showModal = (id) => {
  console.log(id);
  modalId.value = `${id}`;
  openModal.value = true;
};
</script>

<template>
  <h1>Trending Movies!</h1>
  <div class="images">
    <div class="image-container" v-for="movies in trendingMovies">
      <img
        class="moviePosters"
        :src="`https://image.tmdb.org/t/p/w500${movies.poster_path}`"
        :alt="movies.title"
        :props.movieId="`${movies.id}`"
        @click="showModal(movies.id)"
      />
    </div>
  </div>
  <SiteModal :show="openModal" @close="openModal = false" :id="modalId" />
</template>

<style scoped>
.images {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 0.5rem;
}
.image-container {
  display: grid;
  grid-column: span 1;
}
.image-container img {
  width: 100%;
  height: 100%;
}
.moviePosters {
  width: 100%;
  height: 100%;
}
.moviePosters:hover {
  cursor: pointer;
}
</style>