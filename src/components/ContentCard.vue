<template>
  <div
    class="
      content-card
      p-2
      text-center
      d-flex
      flex-column
      justify-content-between
      align-items-center
    "
    :style="backgroundImageInlineStyle"
  >
    <div class="movie-info d-none">
      <h3 class="text-danger">{{ content.title || content.name }}</h3>
      <h4>{{ content.original_title || content.original_name }}</h4>
      <img
        v-if="hasFlag"
        :src="require(`../assets/img/${content.original_language}.png`)"
        :alt="content.original_language"
        class="flag"
      />
      <span v-else>{{ content.original_language }}</span>
      <span>{{ getVote }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentCard",

  props: {
    content: Object,
  },

  computed: {
    backgroundImageInlineStyle() {
      const baseUri = "https://image.tmdb.org/t/p/";
      return `background-image: url("${baseUri}w342${this.content.poster_path}")`;
    },

    hasFlag() {
      const flags = ["it", "en"];
      return flags.includes(this.content.original_language);
    },

    getVote() {
      const vote = this.content.vote_average / 2;
      return Math.ceil(vote);
    },
  },
};
</script>

<style lang="scss" scoped>
.content-card {
  margin: 20px;
  flex-basis: calc(100% / 5 - 40px);
  min-height: 350px;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  background-color: black;
  color: white;
  border: 0.2px solid white;
  box-shadow: 0px 5px 8px black;

  .flag {
    width: 40px;
  }
}
</style>