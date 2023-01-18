<script setup>
import { ref, watch } from "vue";
import axios from "axios";
const props = defineProps({
  show: Boolean,
  id: String,
});
let movie = ref(null);
const getData = async (url, params) => {
  try {
    return await axios.get(url, params);
  } catch (error) {
    console.log(error);
  }
};
const getMovieData = async (movieId) => {
  const extraData = await getData(`https://api.themoviedb.org/3/movie/${movieId}`, {
    params: {
      api_key: "c6b2390c3ab4bfbd0e064d952df483c9",
      append_to_response: "videos",
    },
  });
  console.log(movieId);
  movie.value = extraData.data;
  console.log(movie.value);
};
watch(() => {
  getMovieData(props.id);
});
</script>

<template>
  <div v-if="show" class="modal" @click="$emit('close')">
    <div class="modal-container" @click.stop="">
      <button @click="$emit('close')" class="close-button">X</button>
      <div class="modal-content-container">
        <div class="modal-inner-container">
          <h3 class="movie-title">{{ movie.title }}</h3>
          <p class="movie-overview">{{ movie.overview }}</p>
          <div class="movie-poster">
            <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" />
          </div>
          <div
            class="movie-trailer"
            v-if="
              movie.videos.results.filter((video) => video.type === 'Trailer').length != 0
            "
          >
            <iframe
              :src="`https://www.youtube.com/embed/${
                movie.videos.results.filter((video) => video.type === 'Trailer').at(0).key
              }`"
              frameborder=""
              class="movie-trailer"
            ></iframe>
            <a
              :href="`https://www.youtube.com/watch?v=${
                movie.videos.results.filter((video) => video.type === 'Trailer').at(0).key
              }`"
            >
              <p>Movie Trailer</p>
            </a>
          </div>
          <div class="movie-release-date">
            <h3>Release Date</h3>
            <h4>{{ movie.release_date }}</h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  display: grid;
  position: fixed;
  inset: 0;
  background: #00000099;
}
.modal-container {
  background: white;
  width: 85vw;
  height: 70vh;
  margin: auto;
}
.modal-content-container {
  display: grid;
  width: 100%;
  height: 100%;
}
.modal-inner-container {
  display: grid;
  width: 100%;
  height: 100%;
}
.movie-title {
  grid-column: span 6;
  text-align: center;
  font-size: 180%;
}
.movie-poster {
  grid-column: span 2;
  width: 100%;
  height: 100%;
}
.movie-poster img,
.movie-poster a {
  width: 90%;
  max-width: 200px;
  max-height: 300px;
}
.movie-overview {
  grid-column: span 6;
  text-align: center;
}
.movie-trailer {
  grid-column: span 4;
  text-align: center;
  width: 90%;
  height: 90%;
}
.movie-release-date {
  grid-column: span 2;
  text-align: center;
}
.close-button {
  position: absolute;
  right: 0.5px;
  background: none;
  cursor: pointer;
  background: white;
}
.close-button:hover {
  background: white;
}
</style>