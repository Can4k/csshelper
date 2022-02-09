<template>
  <span @click="clicked"
        class="theme-button-container" :class="[this.$store.state.isDarkTheme? 'dark' : 'white']">
    <strong v-show="this.$store.state.isDarkTheme">LIGHT</strong>
    <strong v-show="!this.$store.state.isDarkTheme">DARK</strong>
  </span>
</template>

<script>
export default {
  name: "ThemeButton",
  methods: {
    clicked() {
      this.$store.state.isDarkTheme = !this.$store.state.isDarkTheme;
      this.$store.state.isDarkTheme?
          document.body.style.backgroundColor = "#121515" : document.body.style.backgroundColor = "white";
    }
  }
}
</script>

<style scoped>
.theme-button-container {
  transition-duration: .5s;
  background-color: #2a2a2c;
  color: white;
  font-family: 'Nunito', sans-serif;
  font-size: 10px;
  border-radius: 4px;
  margin: 2px;
  padding: 2px;
  cursor: pointer;
  user-select: none;
}
.dark {
  background-color: #e1e8e7;
  color: black;
  transition-duration: .4s;
}
.white {
  color: white;
  transition-duration: .4s;
  box-shadow: 0 0 100px;
}
</style>