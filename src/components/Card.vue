<template>
  <div>
    <ul>
      <li>{{ item.title || item.name }}</li>
      <li>{{ item.original_title || item.original_name }}</li>
      <li>
        <img v-if="hasFlag" :src="flagSrc" :alt="item.original_language" />
        <span v-else>{{ item.original_language }}</span>
      </li>
      <li>{{ item.vote_average }}</li>
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
      return require(`../assets/img/${this.item.original_language}.png`);
    },
    hasFlag() {
      return this.flags.includes(this.item.original_language);
    },
  },
};
</script>

<style>
</style>