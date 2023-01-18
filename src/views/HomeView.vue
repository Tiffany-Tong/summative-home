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
  width: 100vw;
  height: 100vh;
}
</style>