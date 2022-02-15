<template>
  <div>
    <header>
      <Search @search="search" />
    </header>
    <main>
      <section id="movies">
        <h2>Movies</h2>
        <Card v-for="movie in movies" :key="movie.id" :item="movie" />
      </section>
      <section id="series">
        <h2>Series</h2>
        <Card v-for="serie in series" :key="serie.id" :item="serie" />
      </section>
    </main>
  </div>
</template>



<script>
import axios from "axios";
import Search from "./components/Search.vue";
import Card from "./components/Card.vue";

export default {
  components: { Search, Card },

  data() {
    return {
      movies: [],
      series: [],
      api: {
        baseUri: "https://api.themoviedb.org/3",
        key: "c7acdad0ed697be61f76da71c493064e",
        lenguage: "it-IT",
      },
    };
  },

  methods: {
    search(word) {
      if (!word) {
        this.movies = [];
        this.series = [];
        return;
      }

      const { key, lenguage } = this.api;
      const config = {
        params: {
          api_key: key,
          query: word,
          lenguage,
        },
      };

      this.fetchApi("search/movie", config, "movies");
      this.fetchApi("search/tv", config, "series");
    },

    fetchApi(endpoint, config, target) {
      axios
        .get(`${this.api.baseUri}/${endpoint}`, config)
        .then((res) => {
          this[target] = res.data.results;
        })
        .catch((err) => {
          console.log(err);
        });
    },
  },
};
</script>



<style lang="scss">
</style>
