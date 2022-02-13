<template>
  <div class="lesson-card-default" :class="[this.$store.state.isDarkTheme? 'dark' : 'light']" @click="openLesson">
    <strong>{{currentObject.header}}</strong>
    <div class="lesson-card-body">
      <span class="tag" v-for="tag in currentObject.tags" :key="tag.name">
        <strong>{{tag}}</strong>
      </span>
      <div class="tag" @click.stop="changeLesson">
        <strong style="color: white; background-color: #3e4444">ИЗМЕНИТЬ ТЕГ</strong>
      </div>
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
    },
    changeLesson() {
      this.$emit("changeLesson", {
        id: this.cardIndex
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
  max-width: 340px;
  min-width: 340px;
  transition-duration: .2s;
}
.light {
  background-color: #e1e8e7;
  color: black;
}
.dark {
  background-color: #292F2F;
  color: #b0b7b6;
}
.light:hover{
  background-color: #d8d8e1;
  cursor: pointer;
}
.dark:hover{
  background-color: #5c6464;
  cursor: pointer;
}
.lesson-card-default strong {
  font-size: 16px;
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
.tag-change {
  transition-duration: 0s;
  display: flex;
  align-items: center;
  justify-content: center;
}
.tag-change strong {
  font-family: 'Nunito', sans-serif;
  font-size: 10px;
  background-color: #42b983;
  border-radius: 4px;
  padding: 1px 2px 1px 2px;
  transition-duration: 0s;
  color: white;
  cursor: pointer;
  user-select: none;
}
.lesson-card-body {
  display: flex;
  align-items: center;
}
</style>