<template>
  <div>
    <ul>
      <li>{{ item.title || item.name }}</li>
      <li>{{ item.original_title || item.original_name }}</li>
      <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language" />
        <span v-else>{{ item.original_language }}</span>
      </li>
      <li>
        <i
          v-for="n in 5"
          :key="n"
          class="fa-star"
          :class="n <= vote ? 'fas' : 'far'"
        ></i>
      </li>
      <li>
        <img :src="posterPath" :alt="item.title || item.name" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],

  data() {
    return {
      flags: ["it", "en"],
      apiImg: {
        baseUri: "http://image.tmdb.org/t/p/w300/",
        placeholder:
          "http://www.theprintworks.com/wp-content/themes/psBella/assets/img/film-poster-placeholder.png",
      },
    };
  },

  computed: {
    flagSrc() {
      return require(`../assets/img/${this.item.original_language}.png`);
    },
    hasFlag() {
      return this.flags.includes(this.item.original_language);
    },
    posterPath() {
      if (!this.item.poster_path) return this.apiImg.placeholder;
      return this.apiImg.baseUri + this.item.poster_path;
    },
    vote() {
      return Math.ceil(this.item.vote_average / 2);
    },
  },
};
</script>

<style>
</style>