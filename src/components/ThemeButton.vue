<template>
  <span @click="clicked"
        class="theme-button-container" :class="[this.$store.state.isDarkTheme? 'dark' : 'white']">
    <strong v-show="this.$store.state.isDarkTheme">to light theme</strong>
    <strong v-show="!this.$store.state.isDarkTheme">to dark theme</strong>
  </span>
</template>

<script>
export default {
  name: "ThemeButton",
  methods: {
    clicked() {
      this.$emit("changeTheme");
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
  font-size: 13px;
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
  box-shadow: 0 0 7px white;
}
.white {
  color: white;
  transition-duration: .4s;
  box-shadow: 0 0 7px black;
}
</style>