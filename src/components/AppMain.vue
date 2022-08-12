<template>
  <main class="p-3">
    <!-- movies section -->
    <section id="movies" class="text-center">
      <h2>Movies</h2>
      <div class="d-flex justify-content-start flex-wrap p-3">
        <ContentCard v-for="movie in movies" :key="movie.id" :content="movie" />
      </div>
    </section>
    <!-- series section -->
    <section id="series" class="text-center">
      <h2>Series</h2>
      <div class="d-flex justify-content-start flex-wrap p-3">
        <ContentCard v-for="serie in series" :key="serie.id" :content="serie" />
      </div>
    </section>
  </main>
</template>

<script>
import ContentCard from "./ContentCard.vue";

export default {
  name: "AppMain",

  components: {
    ContentCard,
  },

  props: {
    movies: Array,
    series: Array,
  },
};
</script>

<style lang="scss" scoped>
main {
  height: calc(100vh - 80px);
  background-color: dimgray;
  overflow: scroll;
}
</style>