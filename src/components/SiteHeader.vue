<script setup>
import { useRouter } from "vue-router";
const router = useRouter();
const login = () => {
  router.push("/login");
};
</script>

<template>
  <h1>Movies Inc.</h1>
  <button @click="login">Login</button>
</template>

<style scoped>
* {
  margin: 0px;
  padding: 0px;
}
h1 {
  display: flex;
  font-size: 70px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
  color: black;
  justify-content: start;
}
button {
  display: flex;
  margin-top: 20px;
  padding: 5px;
  background-color: lightgray;
  position: relative;
  left: 1100px;
  top: -70px;
  width: fit-content;
  height: fit-content;
  font-size: 20px;
}
</style>