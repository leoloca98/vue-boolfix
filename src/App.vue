<template>
  <div id="app">
    <header class="bg-black d-flex justify-content-between align-items-center">
      <h1 class="ms-5 text-danger title-ff">BOOLFLIX</h1>
      <Search class="me-5" @search="getInput" />
    </header>
    <main class="bg-secondary pb-6">
      <Results title="Film" id="film" :items="movies" />
      <Results title="Serie TV" id="serie-tv" :items="serieTv" />
    </main>
  </div>
</template>

<script>
import axios from "axios";
import Search from "@/components/Search.vue";
import Results from "@/components/Results.vue";

export default {
  name: "App",
  components: {
    Search,
    Results,
  },
  data() {
    return {
      movies: [],
      serieTv: [],
    };
  },
  methods: {
    getInput(query) {
      let linkMovie =
        "https://api.themoviedb.org/3/search/movie?api_key=f5d5e3c0ce73a01203b1eaa433c3f0cb&query=" +
        query;
      let linkTv =
        "https://api.themoviedb.org/3/search/tv?api_key=f5d5e3c0ce73a01203b1eaa433c3f0cb&query=" +
        query;

      if (query != "") {
        axios.get(linkMovie).then((res) => (this.movies = res.data.results));
        axios.get(linkTv).then((res) => (this.serieTv = res.data.results));
      }
    },
  },
};
</script>

<style lang="scss">
#app {
  width: 100%;
  margin: 0;
  padding: 0;

  header {
    height: 100px;
    width: 100%;
  }

  main {
    width: 100%;
  }
}

.bg-black {
  background-color: #000;
}

@import "../src/assets/scss/style.scss";
</style>
