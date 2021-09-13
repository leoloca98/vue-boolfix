<template>
  <div class="search-bar">
    <input type="text" placeholder="Inserisci titolo..." v-model="input" />
    <button class="sumbit" @click="sendInput" @keyup.enter="sendInput">
      Search
    </button>
  </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      input: "",
    };
  },
  methods: {
    sendInput() {
      this.$emit("search", this.input);
      this.input = "";
    },
  },
};
</script>

<style scoped lang="scss">
.search-bar {
  margin: 60px 0;
}
</style>