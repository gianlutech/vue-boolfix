<template>
  <div>
    <header class="bg-dark">
      <div
        class="container d-flex justify-content-between align-items-center py-4"
      >
        <h1 class="text-danger">BOOLFIX</h1>
        <Search @search="search" />
      </div>
    </header>
    <main class="bg-grey">
      <div class="container py-4">
        <section id="movies">
          <h2 class="text-danger">Movies</h2>
          <div class="card-settings">
            <Card v-for="movie in movies" :key="movie.id" :item="movie" />
          </div>
        </section>
        <section id="series">
          <h2 class="text-danger">Series</h2>
          <div class="card-settings">
            <Card v-for="serie in series" :key="serie.id" :item="serie" />
          </div>
        </section>
      </div>
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
        language: "it-IT",
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

      const { key, language } = this.api;
      const config = {
        params: {
          api_key: key,
          query: word,
          language,
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
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

main {
  min-height: 100vh;
  background-color: #434343;
}
.card-settings {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  flex-basis: 30%;
}
</style>
