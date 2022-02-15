<template>
  <div>
    <ul>
      <li>{{ item.title || item.name }}</li>
      <li>{{ item.original_title || item.original_name }}</li>
      <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="item.original_lenguage" />
        <span v-else>{{ item.original_lenguage }}</span>
      </li>
      <li>{{ item.vote_avarage }}</li>
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
    };
  },

  computed: {
    flagSrc() {
      return require(`@/assets/img/${this.item.original_lenguage}.png`);
    },
    hasFlag() {
      return this.flags.includes(this.item.original_lenguage);
    },
  },
};
</script>

<style>
</style>