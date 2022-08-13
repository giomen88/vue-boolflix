<template>
  <div class="content-card" :style="backgroundImageInlineStyle">
    <div
      class="
        content-info
        flex-column
        justify-content-between
        align-items-start
        h-100
      "
    >
      <span><strong>Titolo:</strong> {{ content.title || content.name }}</span>
      <span>
        <strong>Titolo Originale:</strong>
        {{ content.original_title || content.original_name }}
      </span>
      <div>
        <strong>Lingua:</strong>
        <img
          v-if="hasFlag"
          :src="require(`../assets/img/${content.original_language}.png`)"
          :alt="content.original_language"
          class="flag ms-1"
        />
        <span v-else class="ms-1">{{ content.original_language }}</span>
      </div>
      <span><strong>Voto:</strong> {{ getVote }}</span>
      <span><strong>Overview:</strong> {{ content.overview }}</span>
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
  height: 350px;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center;
  background-color: black;
  color: white;
  border: 0.2px solid white;
  box-shadow: 0px 5px 8px black;
  cursor: pointer;

  .content-info {
    display: none;
  }
  &:hover .content-info {
    display: flex;
    background-color: black;
    overflow-y: auto;
    padding: 5px;
  }
  .flag {
    width: 40px;
  }
}
</style>