<template>
  <header class="d-flex justify-content-between align-items-center p-2">
    <h1 class="text-danger">BOOLFLIX</h1>
    <BaseSearchBar placeholder="Cerca film..." @search="searchContents" />
  </header>
</template>

<script>
import BaseSearchBar from "./BaseSearchBar.vue";

export default {
  name: "AppHeader",
  components: {
    BaseSearchBar,
  },

  methods: {
    searchContents(searchText) {
      this.$emit("fetch-contents", searchText);
    },
  },
};
</script>

<style lang="scss" scoped>
header {
  height: 80px;
  background-color: black;
}
</style>