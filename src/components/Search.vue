<template>
  <div>
    <div id="input-group" class="d-flex align-items-center">
      <input
        type="text"
        :placeholder="'Digita un titolo...'"
        v-model.trim="word"
        @keyup.enter="goSearch"
        class="p-1 mx-2"
      />
      <button @click="goSearch" class="btn btn-danger">Cerca</button>
    </div>
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