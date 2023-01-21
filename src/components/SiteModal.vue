<script setup>
import axios from "axios";
import { useStore } from "../store/index.js";
const store = useStore();
const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);
let movie = (
  await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
    params: {
      api_key: "c6b2390c3ab4bfbd0e064d952df483c9",
    },
  })
).data;
</script>

<template>
  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <h1>{{ movie.title }}</h1>
        <h2>Overview:</h2>
        <p2>{{ movie.overview }}</p2>
        <h3>Tagline:</h3>
        <p3> {{ movie.tagline }}</p3>
        <h4>Release Date:</h4>
        <p4>{{ movie.release_date }}</p4>
        <div class="movie-poster">
          <img :src="`https://image.tmdb.org/t/p/w500${movie.poster_path}`" />
        </div>
        <button
          @click="
            store.addToCart(props.id, {
              id: movie.id,
              poster: movie.poster_path,
              title: movie.title,
              date: movie.release_date,
            })
          "
        >
          Purchase
        </button>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
}
.modal-outer-container .modal-inner-container {
  background-color: white;
  color: black;
  width: clamp(280px, 100%, 800px);
  height: 400px;
  position: relative;
  width: 60vw;
  height: 100vh;
  margin: auto;
  display: grid;
  grid-column: 4;
}
.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: white;
  font-weight: bold;
  font-size: 1.25rem;
  color: black;
}
img {
  width: 280px;
  height: 400;
  float: unset;
}
</style>