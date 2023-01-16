<script setup></script>

<template>
  <div class="image-container">
    <div class="text-container">
      <h2>Enjoy learning about different movies!</h2>
      <p>Ready to learn about movies you might enjoy watching?</p>
      <p2>Click the "Login" button on top to get started!</p2>
    </div>
    <img
      src="https://hips.hearstapps.com/hmg-prod.s3.amazonaws.com/images/patriotic-movies-1656601992.jpg?crop=0.934xw:1.00xh;0.0337xw,0&resize=980:*"
    />
  </div>
</template>

<style scoped>
img {
  width: 130%;
  margin-left: -50px;
}
.image-container {
  position: relative;
  text-align: start;
  color: white;
  text-size-adjust: 100px;
  font-family: "Times New Roman", Times, serif;
  font-size: x-large;
  left: -300px;
}
.text-container {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: black;
}
</style>