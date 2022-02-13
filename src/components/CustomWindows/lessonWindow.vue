<template>
  <div v-show="isActive">
    <div class="information-content" :class="[this.$store.state.isDarkTheme? 'dark' : 'light']">
       <h2>{{ currentObject.header }}</h2>
      <div v-for="i in currentObject.body" class="information-field">
        <b>{{ i }}</b>
      </div>
      <footer>
        <div class="ok-button" @click="closeLesson">
          <h3>ОК</h3>
        </div>
      </footer>
    </div>
  </div>
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
  },
  methods: {
    closeLesson() {
      this.$emit("closeLesson");
    }
  }
}
</script>

<style scoped>
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
  margin-bottom: 20px;
}

.information-field {
  font-size: 15px;
  margin-bottom: 10px;
}

.information-content footer {
  display: flex;
  justify-content: center;
}

.ok-button {
  background-color: #008cff;
  color: white;
  padding: 2px 20px 2px 20px;
  border-radius: 4px;
  margin-top: 10px;
  user-select: none;
  transition-duration: .2s;
}

.ok-button:hover {
  transform: scale(1.05);
  cursor: pointer;
}

@media screen and (max-width: 740px) {
  .information-content {
    background-color: white;
    border-radius: 10px;
    padding: 10px;
    font-family: 'Nunito', sans-serif;
    z-index: 2;
    max-width: 350px;
    min-width: 310px;
  }

}
</style>