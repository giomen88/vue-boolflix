<template>
  <div>
    <AppHeader @fetch-contents="startSearch" />
    <AppMain :movies="movies" :series="series" />
  </div>
</template>

<script>
import axios from "axios";
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";

export default {
  components: {
    AppHeader,
    AppMain,
  },

  data() {
    return {
      movies: [],
      series: [],

      api: {
        key: "d45c4b49da1f7e6c04a4b082cd11af80",
        baseUri: "https://api.themoviedb.org/3",
        language: "it-IT",
      },
    };
  },

  methods: {
    startSearch(query) {
      if (!query) {
        this.movies = this.series = [];
        return;
      }

      const config = {
        params: {
          api_key: this.api.key,
          language: this.api.language,
          query,
        },
      };

      this.fetchData("/search/movie", config, "movies");
      this.fetchData("/search/tv", config, "series");
    },

    fetchData(endpoint, config, request) {
      axios.get(`${this.api.baseUri}${endpoint}`, config).then((res) => {
        this[request] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
@import "./assets/sass/style.scss";
</style>
