<template>
  <div class="alert-container" :class="[this.$store.state.isDarkTheme? 'dark' : 'light']">
    <strong :style="[type ==='warn' ? 'color: #b82020' : 'color: black']">{{text}}</strong>
  </div>
</template>

<script>
export default {
  name: "AlertComponent",
  props: {
    type: String,
    text: String
  },
}
</script>

<style scoped>
.alert-container {
  font-size: 16px;
  position: fixed;
  border: 2px solid red ;
  border-radius: 5px;
  padding: 7px;
  font-family: 'Nunito', sans-serif;
  top: 10px;
  left: 75%;
  margin: 10px;
  text-align: center;
  opacity: 85%;
  text-transform: uppercase;
  z-index: 5;
}
.dark {
  background-color: #0b1117ff;
}
.light {
  background-color: white;
}
@media screen and (max-width: 800px){
  .alert-container {
    font-size: 15px;
    text-align: center;
    top: 0;
    margin: 5px;
    left: 50%;
    padding: 2px;
  }
}
</style>