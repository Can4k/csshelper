<template>
  <div class="main-container">
    <h2 :class="[this.$store.state.isDarkTheme? 'dark-h2' : '']">Фильтр тегов</h2>
    <searcher @updateList="updateList"/>
    <h2 :class="[this.$store.state.isDarkTheme? 'dark-h2' : '']">Список всей теории</h2>
    <transition-group name="list">
      <div v-for="i in currentLessonList" class="lessons-container">
        <lesson-card @openLesson="openWindow" :card-index="i.id"/>
      </div>
    </transition-group>
  </div>
  <lesson-window @closeLesson="closeWindow" :is-active="isLessonOpen" :lesson-number="selectedNumber"/>
  <div class="telegram-logo">
    <theme-button/>
  </div>
</template>

<script>
import LessonCard from "@/components/LessonCard";
import LessonWindow from "@/components/lessonWindow";
import Searcher from "@/components/Searcher";
import ThemeButton from "@/components/ThemeButton";

export default {
  name: "Directory",
  components: {ThemeButton, Searcher, LessonWindow, LessonCard},
  methods: {
    openWindow(data) {
      this.selectedNumber = data.lessonIndex;
      this.isLessonOpen = true;
    },
    closeWindow() {
      this.isLessonOpen = false;
    },
    updateList() {
      this.currentTagsList = [];
      this.currentLessonList = [];
      for (var tag of this.$store.state.activeTags) {
        if (tag.isActive) {
          this.currentTagsList.push(tag.name);
        }
      }
      for (let i = 0; i < this.LessonList.length; i++) {
        var flag = false;
        for (let j = 0; j < this.currentTagsList.length; j++) {
          flag |= (this.LessonList[i].tags.indexOf(this.currentTagsList[j]) === -1);
        }
        console.log(`${i} ${flag}`);
        if (flag == 0) {
          this.currentLessonList.push(this.LessonList[i]);
        }
      }
      console.log(this.currentLessonList);
    }
  },
  data() {
    return {
      isLessonOpen: false,
      selectedNumber: -1,
      currentLessonList: {},
      currentTagsList: [],
      LessonList: {}
    }
  },
  mounted() {
    this.LessonList = this.$store.state.LessonsList;
    this.updateList();
  },
}
</script>

<style scoped>
.main-container {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.main-container h2 {
  font-family: 'Nunito', sans-serif;
  font-size: 30px;
  text-align: center;
  margin: 20px;
  user-select: none;
}

.main-container .dark-h2 {
  color: #b0b7b6;
}

.lessons-container {
  display: flex;
}

.telegram-logo{
  position: fixed;
  left: 4px;
  top: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.telegram-logo img{
  margin: 4px;
}

.telegram-logo strong {
  font-family: 'Nunito', sans-serif;
  font-weight: 1000;
  font-size: 10px;
  color: black;
}

.telegram-logo-dark {
  color: #e1e8e7;
}

a:visited {
  text-decoration: none;
  color: #008cff;
}
.telegram-logo-dark strong{
  color: white;
}
.telegram-logo-dark strong{
  color: white;
}
a:hover {
  text-decoration: none;
  color: darkblue;
}

a{
  text-decoration: none;
  transition-duration: .2s;
}

.list-enter-active,
.list-leave-active {
  transition: all .2s;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
}
</style>