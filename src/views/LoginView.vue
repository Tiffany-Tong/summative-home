<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const username = ref("");
const password = ref("");
const error = ref(false);

const login = () => {
  if (username.value === "tmdb" && password.value === "movies") {
    router.push("/purchase");
  } else {
    error.value = true;
  }
};
</script>

<template>
  <div class="login-container">
    <h1>Login</h1>
    <form @submit.prevents="login()">
      <input type="text" v-model="username" placeholder="Username" />
      <input type="password" v-model="password" placeholder="Password" />
      <input type="submit" value="Login" />
    </form>
    <div v-if="error" class="error">
      <p>Wrong username or password.</p>
    </div>
  </div>
</template>

<style scoped>
.home-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100vw;
  height: 100vh;
  font-size: 4rem;
}
form {
  display: flex;
  flex-direction: column;
}
form input {
  padding: 0.25rem;
  color: black;
  font-size: 1.5rem;
  font-weight: bold;
}
</style>