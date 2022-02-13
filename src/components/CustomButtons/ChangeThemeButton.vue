<template>
    <button @click="this.$emit('changeTheme')" class="theme-button-container" :class="[this.$store.state.isDarkTheme? 'dark' : 'light']">
      <strong>{{this.$store.state.isDarkTheme? "В ДЕНЬ" : "В НОЧЬ"}}</strong>
    </button>
</template>

<script>
export default {
  name: "ChangeThemeButton",
}
</script>

<style scoped>
.theme-button-container {
  font-family: 'Nunito', sans-serif;
  font-size: 13px;
  border-radius: 10px;
  margin: 2px;
  padding: 4px;
  cursor: pointer;
  user-select: none;
  border: none;
}
.theme-button-container:hover, :focus{
  transform: scale(1.05);
}
.dark {
  background-color: #e1e8e7;
  color: black;
  box-shadow: 0 0 7px white;
}
.light {
  background-color: #2a2a2c;
  color: white;
  box-shadow: 0 0 7px black;
}
* {
  transition-duration: .2s;
}
</style>