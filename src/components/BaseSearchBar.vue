<template>
  <div class="search-bar">
    <input
      type="text"
      class="me-2 rounded border-0 p-2"
      :placeholder="placeholder"
      v-model.trim="searchText"
      @keyup.enter="emitSearch"
    />
    <button class="rounded border-0 py-2 px-4" @click="emitSearch">
      Cerca
    </button>
  </div>
</template>

<script>
export default {
  name: "BaseSearchBar",

  props: {
    placeholder: String,
  },

  data() {
    return {
      searchText: "",
    };
  },

  methods: {
    emitSearch() {
      this.$emit("search", this.searchText);
    },
  },
};
</script>

<style lang="scss" scoped>
</style>