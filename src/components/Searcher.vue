<template>
  <div class="filter-container">
    <div class="searcher-container"
         :class="[this.$store.state.isDarkTheme? 'dark' : 'light']">
    <span class="tag" v-for="tag in activeTags">
        <strong v-show="this.$store.state.isDarkTheme" :class="[tag.isActive? 'on-tag-d' : 'off-tag-d']" @click="log(tag)">{{tag.name}}</strong>
        <strong v-show="!this.$store.state.isDarkTheme" :class="[tag.isActive? 'on-tag' : 'off-tag']" @click="log(tag)">{{tag.name}}</strong>
    </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "Searcher",
  data() {
    return {
      activeTags: {}
    }
  },
  mounted() {
    this.activeTags = this.$store.state.activeTags;
  },
  methods: {
    log(data) {
      data.isActive = !data.isActive;
      this.$emit("updateList");
    }
  }
}
</script>

<style scoped>
.tag strong {
  font-family: 'Nunito', sans-serif;
  font-size: 10px;
  border-radius: 4px;
  padding: 1px 2px 1px 2px;
  display: flex;
  align-items: center;
  margin: 3px;
  }
.searcher-container{
  display: flex;
  width: 370px;
  background-color: #e1e8e7;
  border-radius: 4px;
  margin: 0;
  flex-wrap: wrap;
  justify-content: center;
  padding: 4px;
}
.filter-container {
  display: flex;
}
.searcher-container h2{
  font-family: 'Nunito', sans-serif;
  font-size: 50px;
  text-align: center;
}
.tag strong {
  cursor: pointer;
  user-select: none;
}
.on-tag {
  display: flex;
  align-items: center;
  background-color: #42b983;
}
.off-tag {
  display: flex;
  align-items: center;
  background-color: #d6d9d0;
}
.dark {
  background-color: #292F2F;
  color: black;
}
.off-tag-d {
  background-color: #4c5656;
}.on-tag-d {
  color: black;
  background-color: #42b983;
 }
</style>