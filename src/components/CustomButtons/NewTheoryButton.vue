<template>
  <div class="theme-button-container">
    <strong :style="[this.$store.state.isDarkTheme? 'color: white' : 'color: black']">+</strong>
  </div>
</template>

<script>
export default {
  name: "NewTheoryButton",
}
</script>

<style scoped>
.theme-button-container strong{
  font-family: 'Nunito', sans-serif;
  font-size: 20px;
  border-radius: 5px;
  padding: 0 7px 0 7px;
  user-select: none;
  cursor: pointer;
  background-color: #42b983;
}
.theme-button-container strong:hover {
  background-color: #5c6464;
}
</style>