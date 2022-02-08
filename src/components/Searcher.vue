<template>
  <div class="filter-container">
    <div class="searcher-container">
    <span class="tag" v-for="tag in activeTags" @click="log(tag)">
        <strong :class="[tag.isActive? 'on-tag' : 'off-tag']">{{tag.name}}</strong>
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
  margin: 3px;
  }
.searcher-container{
  display: flex;
  width: 400px;
  background-color: #e1e8e7;
  border-radius: 4px;
  margin: 0;
  flex-wrap: wrap;
  justify-content: center;
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
  margin: 7px;
  cursor: pointer;
  user-select: none;
}
.on-tag {
  display: flex;
  justify-self: start !important;
  align-items: center;
  background-color: #42b983;
}
.off-tag {
  display: flex;
  justify-self: start !important;
  align-items: center;
  background-color: #d6d9d0;
}
</style>