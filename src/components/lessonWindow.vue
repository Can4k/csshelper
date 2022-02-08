<template>
  <transition name="fade">
    <div v-show="isActive" class="lesson-window-content">
      <div class="information-content">
        <h2>{{currentObject.header}}</h2>
        <div v-for="i in currentObject.body">
          <b>{{i}}</b>
        </div>
        <footer>
          <div class="ok-button" @click="closeLesson">
            <h3>ОК</h3>
          </div>
        </footer>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "lessonWindow",
  props: {
    isActive: Boolean,
    lessonNumber: Number
  },
  data() {
    return {
      currentObject: {}
    }
  },
  updated() {
    this.currentObject = this.$store.state.LessonsList[this.lessonNumber];
    //console.log(this.currentObject);
  },
  methods: {
    closeLesson() {
      this.$emit("closeLesson");
    }
  }
}
</script>

<style scoped>
.lesson-window-content {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  transition-duration: 4s;
  background-color: #d8d8e1;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity .2s;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
.information-content {
  margin-top: 50px;
  background-color: white;
  position: absolute;
  left: 50%;
  transform: translate(-50%);
  border-radius: 10px;
  padding: 10px;
  font-family: 'Nunito', sans-serif;
  z-index: 2;
}
.information-content h2 {
  text-align: center;
  margin-bottom: 5px;
}
.information-content b {
  font-size: 13px;
}
.information-content footer {
  display: flex;
  justify-content: center;
}
footer h3 {
  background-color: #008cff;
  color: white;
  padding: 2px 20px 2px 20px;
  border-radius: 4px;
  margin-top: 10px;
  user-select: none;
  transition-duration: .2s;
}
footer h3:hover {
  transform: scale(1.05);
  cursor: pointer;
}
@media screen and (max-width: 740px){
  .information-content {
    background-color: white;
    border-radius: 10px;
    padding: 10px;
    font-family: 'Nunito', sans-serif;
    z-index: 2;
    max-width: 700px;
    min-width: 370px;
  }
  .lesson-window-content{
    height: 110%;
  }
}
</style>