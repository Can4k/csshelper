<template>
  <div class="lesson-card-default"
       :class="[this.$store.state.isDarkTheme? 'lesson-card-dark' : 'lesson-card-light']"
       @click="openLesson">
    <strong>{{currentObject.header}}</strong>
    <div class="lesson-card-body">
      <span class="tag" v-for="tag in currentObject.tags">
        <strong>{{tag}}</strong>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "LessonCard",
  props: {
    cardIndex: Number
  },
  data() {
    return {
      currentObject: {}
    }
  },
  mounted() {
    this.currentObject = this.$store.state.LessonsList[this.cardIndex];
  },
  updated() {
    this.currentObject = this.$store.state.LessonsList[this.cardIndex];
  },
  methods: {
    openLesson() {
      //console.log(`Opening the lesson number ${this.cardIndex}`);
      this.$emit("openLesson", {
        lessonIndex: this.cardIndex
      })
    }
  }
}
</script>

<style scoped>
.lesson-card-default {
  color: #2a2a2c;
  border-radius: 4px;
  padding: 4px;
  margin: 10px;
  max-width: 370px;
  min-width: 370px;
  transition-duration: .2s;
}
.lesson-card-light {
  background-color: #e1e8e7;
  color: black;
}
.lesson-card-dark {
  background-color: #292F2F;
  color: #b0b7b6;
}
.lesson-card-light:hover{
  background-color: #d8d8e1;
  cursor: pointer;
}
.lesson-card-dark:hover{
  background-color: #5c6464;
  cursor: pointer;
}
.lesson-card-default strong {
  font-size: 17px;
  font-family: 'Nunito', sans-serif;
  font-weight: 900;
  user-select: none;
}
.tag strong {
  font-family: 'Nunito', sans-serif;
  font-size: 10px;
  background-color: #42b983;
  border-radius: 4px;
  padding: 1px 2px 1px 2px;
  transition-duration: 0s;
  color: black;
}
.tag {
  margin: 1px 2px 1px 2px;
  transition-duration: 0s;
}
.lesson-card-body {
  display: flex;
}
</style>