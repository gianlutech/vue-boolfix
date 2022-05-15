<template>
  <div class="card">
    <ul class="">
      <li>
        <h5>{{ item.title || item.name }}</h5>
      </li>
      <li>
        <h5>{{ item.original_title || item.original_name }}</h5>
      </li>
      <li>
        <img
          class="card-img"
          :src="posterPath"
          :alt="item.title || item.name"
        />
      </li>
      <div class="value">
        <li class="w-10">
          <img
            v-if="hasFlag"
            :src="flagSrc"
            :alt="item.original_language"
            class="img-fluid"
          />
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
      </div>
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

<style lang="scss">
.card {
  width: 300px;
  height: 500px;
  padding: 20px;
  margin: 15px 10px;
  background-color: #212529;
  justify-content: center;
  align-items: center;
  box-shadow: 1px 1px 10px 3px #000000;
  cursor: pointer;
}
.card:hover {
  transform: scale(1.1);
  transition: transform 0.2s;
}
.card-img {
  width: 100%;
  height: 300px;
}
ul {
  padding: 0;
  li {
    list-style-type: none;
    font-size: 16px;
    color: white;
    padding: 3px 0;
    i {
      color: #ffbd00;
    }
  }
}
.w-10 {
  width: 10%;
}
.value {
  display: flex;
  justify-content: space-around;
  padding: 10px 0;
}
</style>