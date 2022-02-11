<template>
  <div class="alert-container">
    <strong :style="[type==='or' ? 'color: red' : 'color: black']">{{text}}</strong>
  </div>
</template>

<script>
export default {
  name: "AlertComponent",
  props: {
    type: String,
    text: String
  }
}
</script>

<style scoped>
.alert-container {
  z-index: 10;
  font-size: 15px;
  position: fixed;
  background-color: #e1e8e7;
  border-radius: 3px;
  padding: 5px;
  font-family: 'Nunito', sans-serif;
  left: 70%;
  top: 10px;
}
@media screen and (max-width: 700px){
  .alert-container {
    font-size: 10px;
    text-align: center;
    top: 5px;
    left: 50%;
    transform: translate(-50%);
  }
}
strong {
}
</style>