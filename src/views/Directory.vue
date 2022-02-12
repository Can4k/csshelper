<template>
  <div class="main-container">
    <transition :name="this.$store.state.deviceWidth > 700? 'alert' : 'alert-smart'">
      <alert-component v-show="isAdminWarnOpen" text="Добавлять посты может только админ" type="warn"/>
    </transition>
    <lesson-window @closeLesson="closeWindow" :is-active="isLessonOpen" :lesson-number="selectedNumber"/>
    <admin-window @closeWindow="closeAdmin"
                  :change-obj="changeNumber"
                  :is-active="this.isAdminWindowOpen"/>
    <div class="content-list" v-show="!this.isLessonOpen && !this.isAdminWindowOpen">
      <h2 style="margin-top: 30px" :class="[this.$store.state.isDarkTheme? 'dark-h2' : 'aboba']">Фильтр тегов</h2>
      <searcher @updateList="updateList"/>
      <div class="theory-header">
        <h2 :class="[this.$store.state.isDarkTheme? 'dark-h2' : 'aboba']">Список всей теории</h2>
        <span @click="openAdmin">
          <new-theory-button style="margin-top: 3px"/>
        </span>
      </div>
      <div v-show="!currentLessonList.length" class="alert">
        <strong>нет подходящей теории</strong>
      </div>
      <div v-for="i of this.$store.state.LessonsList" class="lessons-container" :key="i.id">
        <transition name="fade">
          <lesson-card v-show="this.currentLessonList.indexOf(i) !== -1" @changeLesson="changeLesson"
                       @openLesson="openWindow" :card-index="i.id"/>
        </transition>
      </div>
    </div>
  </div>
  <div class="telegram-logo">
    <theme-button @changeTheme="changeTheme"/>
  </div>
</template>

<script>
import LessonCard from "@/components/LessonCard";
import LessonWindow from "@/components/lessonWindow";
import Searcher from "@/components/Searcher";
import ThemeButton from "@/components/ThemeButton";
import NewTheoryButton from "@/components/NewTheoryButton";
import AlertComponent from "@/components/AlertComponent";
import AdminWindow from "@/components/AdminWindow";


export default {
  name: "Directory",
  components: {AdminWindow, AlertComponent, NewTheoryButton, ThemeButton, Searcher, LessonWindow, LessonCard},
  methods: {
    openWindow(data) {
      //console.log(this.currentLessonList);
      //console.log(this.LessonList);
      this.selectedNumber = data.lessonIndex;
      this.isLessonOpen = true;
      if (!this.$store.state.isDarkTheme) {
        document.body.style.backgroundColor = "lightgrey";
      }
    },
    closeWindow() {
      this.isLessonOpen = false;
      if (!this.$store.state.isDarkTheme) {
        document.body.style.backgroundColor = "white";
      }
    },
    updateList() {
      this.currentTagsList = [];
      this.currentLessonList = [];
      for (var tag of this.$store.state.activeTags) {
        if (tag.isActive) {
          this.currentTagsList.push(tag.name);
        }
      }
      for (var i = 0; i < this.$store.state.LessonsList.length; i++) {
        var flag = false;
        for (var j = 0; j < this.currentTagsList.length; j++) {
          flag |= (this.$store.state.LessonsList[i].tags.indexOf(this.currentTagsList[j]) === -1);
        }
        //console.log(`${i} ${flag}`);
        if (flag == 0) {
          this.currentLessonList.push(this.$store.state.LessonsList[i]);
        }
      }
      //console.log(this.currentLessonList);
    },
    changeTheme() {
      this.$store.state.isDarkTheme = !this.$store.state.isDarkTheme;
      if (this.isLessonOpen || this.isAdminWindowOpen) {
        var color;
        this.$store.state.isDarkTheme ? color = '#0b1117' : color = 'lightgrey';
        document.body.style.background = color;
      } else {
        var color;
        this.$store.state.isDarkTheme ? color = '#0b1117' : color = 'white';
        document.body.style.background = color;
      }
    },
    openAdmin() {
      this.changeNumber = {
        body: [],
        header: ""
      };
      if (!this.$store.state.isDarkTheme) {
        document.body.style.backgroundColor = "lightgrey";
      }
      this.isAdminWindowOpen = true;
    },
    closeAdmin() {
      this.updateList();
      if (!this.$store.state.isDarkTheme) {
        document.body.style.backgroundColor = "white";
      }
      this.isAdminWindowOpen = false;
    },
    warnAdmin() {
      if (this.isAdminWarnOpen) {
        return;
      }
      this.isAdminWarnOpen = true;
      setTimeout(() => {
        this.isAdminWarnOpen = false;
      }, 2000)
    },
    changeLesson(data) {
      if (!this.$store.state.isDarkTheme) {
        document.body.style.backgroundColor = "lightgrey";
      }
      this.changeNumber = this.$store.state.LessonsList[data.id];
      this.isAdminWindowOpen = true;
    },
    async getRequest() {
      if (this.$store.state.isProduction) {
        this.$store.state.LessonsList = await fetch('http://localhost:7777')
            .then((response) => {
              return response.json();
            });
        this.updateList();
      } else {
        this.$store.state.LessonsList = [
          {
            id: 0,
            header: "Стили для работы с текстовой информацией",
            tags: ["CSS", "Текст", "HTML", "База", "Позиционирование"],
            body: [
              "color: - цвет [RGB, RGBA, HEX ....]",
              "font-family: - семья шрифта [sans-serif, ...]",
              "font-size: - размер шрифта [px, rem ...]",
              "font-style: - стиль шрифта [normal, italic, oblique];",
              "font-weight: - ширина текста [100 - 1000];",
              "text-align: - выравнивание текста [right, left, center, justify];",
              "text-decoration: - оформление текста [underline, overline, line-through, none];",
              "text-shadow: - эффект тени теста [left, right, down, size, color];",
              "text-transform: - преобразование текста [capitalize, lowercase, uppercase];",
              "text-indent: - размер красной строки;",
              "letter-spacing: - расстояния между символами;",
              "word-spacing: - расстояние между словами;",
              "white-space: nowrap; - весь текст в одну строку;",
              "line-height: - расстояние между строками;",
            ]
          },
          {
            id: 1,
            header: "Псевдоклассы",
            tags: ["Псевдоклассы", "HTML", "CSS"],
            body: [
              ":hover - сработает при наведении;",
              ":visited - сработает, если тег <a> был посещен;",
              ":focus - срабатывает когда выбранно поле;",
              ":first-child - обращение к первому элементу в блоке;",
              ":last-child - обращение к последнему элементу в блоке;"
            ]
          },
          {
            id: 2,
            header: "Псевдоэлементы",
            tags: ["Псевдоэлементы", "HTML", "CSS"],
            body: [
              ":first-line - задает стиль первой строки;",
              ":first-letter - задает стиль первой буквы;",
              ":before - добавляет элемент, заданый в поле content перед содержимым блока;",
              ":after - добавляет элемент, заданый в поле content после содержимым блока;",
            ]
          },
          {
            id: 3,
            header: "Работа с позиционированием",
            tags: ["База", "Позиционирование", "HTML", "CSS"],
            body: [
              "margin: 0 auto - застовляет элемент выстроиться по середине экрана;",
              "position: static - по-умолчанию;",
              "position: relative - позволяет позиционировать элемент отноносительно родителя;",
              "position: absolute - блок становится строчным, не зависит от других блоков;",
              "position: fixed - вырывает блок и фиксирует его относительно браузера;",
              "z-index: контроль порядка элеметов по оси z;"
            ]
          },
          {
            id: 4,
            header: "Работа с display:flex",
            tags: ["Flex", "Позиционирование", "HTML", "CSS"],
            body: [
              "display: flex - \"включает\" flex разметку;",
              "display: inline-flex - строчный flex;",
              "justify-content: - определяет выравнивание вдоль основной оси [flex-start, flex-end, center, space-between, space-around];",
              "align-items: - определят поведение вдоль поперечной оси [stretch, flex-start, flex-end, center];",
              "flex-wrap: - задает правило переноса блоков [nowrap, wrap, reverse-wrap];",
              "flex-direction: - задает основную ось [row, column];"
            ]
          },
          {
            id: 5,
            header: "Display:flex для flex-item",
            tags: ["Flex", "HTML", "CSS", "Позиционирование"],
            body: [
              "flex-align: - тоже самое что align-items;",
              "order: очередь вывода;",
              "flex-basis: - базовое значение размера flex-item;",
              "flex-grow: возможность увеличиваться flex-item больше, чем flex-basis;",
              "flex-shrink: возможность уменьшаться flex-item меньше чем flex-basis;"
            ]
          },
          {
            id: 6,
            header: "Переходы. Transition",
            tags: ["Transition", "HTML", "CSS", "База", "Позиционирование"],
            body: [
              "transition-duration: время переходы;",
              "transition-property: к каким свойствам должны применяться переходы;",
              "transition-delay: задержка перехода;",
              "transition-timing-function: - вид перехода [ease, ease-in, ease-out, ease-in-out, linear ...];",
            ]
          },
          {
            id: 7,
            header: "Изменение блока. Transform",
            tags: ["Transform", "HTML", "CSS", "База", "Позиционирование"],
            body: [
              "translate(x, y) - изменение позиции;",
              "scale(w, h) - изменение размера;",
              "rotate(x deg) - поворот на deg градусов;",
              "transition-timing-function: - вид перехода [ease, ease-in, ease-out, ease-in-out, linear ...];",
            ]
          },
          {
            id: 8,
            header: "Задний фон. Background",
            tags: ["Background", "HTML", "CSS", "База", "Позиционирование"],
            body: [
              "background-color, background-image - задниний цвет, фоновое изображение;",
              "background-repeat: none, repeat-x, repeat-y, space, round(без обрезки) - метод повтра кортинки;",
              "background-position: - позиция фона;",
              "background-attachment: fixed, - фон стоит на одном месте, очень круто;",
              "background-size: - размер фона [cover];"
            ]
          },
        ]
      }
    }
  },
  data() {
    return {
      isLessonOpen: false,
      isAdminWarnOpen: false,
      isAdminWindowOpen: false,
      selectedNumber: -1,
      changeNumber: {},
      currentLessonList: {},
      currentTagsList: [],
    }
  },
  mounted() {
    this.getRequest();
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
  margin: 10px;
  user-select: none;
}

.main-container .dark-h2 {
  color: #b0b7b6;
}

.lessons-container {
  display: flex;
}

.theory-header {
  display: flex;
  align-items: center;
  justify-content: center;
}

.telegram-logo {
  position: fixed;
  left: 4px;
  top: 4px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.telegram-logo img {
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

.telegram-logo-dark strong {
  color: white;
}

.telegram-logo-dark strong {
  color: white;
}

a:hover {
  text-decoration: none;
  color: darkblue;
}

a {
  text-decoration: none;
  transition-duration: .2s;
}

.alert {
  font-family: 'Nunito', sans-serif;
  font-size: 10px;
  text-align: center;
  margin-top: -15px;
  color: red;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity .2s;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.alert-enter-to {
  top: 10px;
}

.alert-enter-from {
  top: -50px;
}

.alert-leave-to {
  margin-top: -50px;
}

.alert-smart-enter-to {
  top: 5px;
}

.alert-smart-enter-from {
  top: -20px;
}

.alert-smart-leave-to {
  margin-top: -30px;
}
</style>