<template>
  <div class="theme-button-container">
    <strong :class="[this.$store.state.isDarkTheme? 'b-d' : 'b-l']">+</strong>
  </div>
</template>

<script>
export default {
  name: "NewTheoryButton",
  methods: {
  }
}
</script>

<style scoped>
.theme-button-container strong{
  z-index: 3;
  font-family: 'Nunito', sans-serif;
  font-size: 20px;
  border-radius: 20px;
  padding: 1px 8px 1px 8px;
  user-select: none;
  font-weight: 1000;
  cursor: pointer;
}
.theme-button-container strong:hover {
  background-color: #5c6464;
}
.b-l {
  background-color: #42b983;
  color: white;
}
.b-d {
  background-color: #42b983;
  color: black;
}
</style>