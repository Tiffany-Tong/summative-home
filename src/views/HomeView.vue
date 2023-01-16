<script setup>
import SiteHeader from "../components/SiteHeader.vue";
import SiteHero from "../components/SiteHero.vue";
import SiteFooter from "../components/SiteFooter.vue";
</script>

<template>
  <div class="home-container">
    <SiteHeader />
    <SiteHero />
    <SiteFooter />
  </div>
</template>

<style scoped>
.home-container {
  /* display: flex;
  flex-direction: row;
  align-items: start;
  justify-content: start; */
  width: 100vw;
  height: 100vh;
}
</style>