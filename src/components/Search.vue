<template>
  <div>
    <input
      type="text"
      :placeholder="'Digita un titolo...'"
      v-model.trim="word"
      @keyup.enter="goSearch"
    />
    <button @click="goSearch">Cerca</button>
  </div>
</template>

<script>
export default {
  name: "Search",

  data() {
    return {
      word: "",
    };
  },

  methods: {
    goSearch() {
      this.$emit("search", this.word);
    },
  },
};
</script>

<style>
</style>