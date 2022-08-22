<template>
  <div class="content-card" :style="backgroundImageInlineStyle">
    <div class="content-info">
      <span>
        <strong>Titolo:</strong>
        {{ content.title || content.name }}
      </span>
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
      <div>
        <strong>Voto:</strong>
        <FontAwesomeIcon v-for="n in 5" :key="n" :icon="renderStar(n)" />
      </div>
      <span>
        <strong>Overview:</strong>
        {{ content.overview }}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentCard",

  props: {
    content: Object,
  },

  data() {
    return {};
  },

  computed: {
    backgroundImageInlineStyle() {
      const baseUrl = "https://image.tmdb.org/t/p/";
      return `background-image: url("${baseUrl}w342${this.content.poster_path}")`;
    },

    hasFlag() {
      const flags = ["it", "en", "es", "ja", "fr", "de"];
      return flags.includes(this.content.original_language);
    },

    vote() {
      return Math.ceil(this.content.vote_average / 2);
    },
  },
  methods: {
    renderStar(n) {
      const iconType = this.vote >= n ? "fa-solid" : "fa-regular";
      return iconType + " fa-star";
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

    ul {
      list-style-type: none;
      // display: flex;
    }
  }
  &:hover .content-info {
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    align-items: flex-start;
    background-color: black;
    padding: 5px;
    overflow-y: scroll;
    text-align: start;
  }
  .flag {
    width: 30px;
    height: 20px;
  }
}
</style>