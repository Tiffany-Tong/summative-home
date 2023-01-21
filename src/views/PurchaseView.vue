<script setup>
import { ref } from "vue";
import SiteModal from "../components/SiteModal.vue";
import { useStore } from "../store/index.js";
const store = useStore();
const genre = ref(10751);
const showModal = ref(false);
const selectedId = ref(0);
const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};
const closeModal = () => {
  showModal.value = false;
};
const getGenres = async () => {
  await store.getMovies(genre.value);
};
</script>

<template>
  <h1>Find A Movie!</h1>
  <div class="cart-button">
    <RouterLink to="/cart" custom v-slot="{ navigate }">
      <button @click="navigate" role="link">Cart</button>
    </RouterLink>
  </div>
  <select v-model="genre" @change="getGenres()">
    <option value="10751">Family</option>
    <option value="12">Adventure</option>
    <option value="35">Comedy</option>
    <option value="28">Action</option>
    <option value="9648">Mystery</option>
  </select>
  <div class="purchase-container">
    <img
      v-for="movie in store.movies"
      :id="movie.id"
      @click="openModal(movie.id)"
      :src="`https://image.tmdb.org/t/p/w500${movie.poster}`"
    />
    <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
  </div>
</template>

<style scoped>
.purchase-container {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 1rem;
}
img {
  width: 200px;
  aspect-ratio: 2 / 3;
}
.cart-button {
  position: absolute;
  left: 1180px;
  top: 70px;
}
</style>