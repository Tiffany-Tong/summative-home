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
    <form @submit.prevent="login()">
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
.login-container {
  margin-top: 20%;
  margin-left: 30%;
}
form {
  display: flex;
  flex-direction: column;
  position: absolute;
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}
form input {
  padding: 0.25rem;
  color: black;
  font-size: 1.5rem;
  font-weight: bold;
}
</style>