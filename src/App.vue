<template>
  <div id="app" class="text-center">
    <Search @search="getInput" />
    <Container />
    <section id="Content">
      <!-- Results -->
      <div class="container">
        <div class="row">
          <div id="film" class="col-6 border border-black h-100">
            <Movies />
            <h2 class="mb-3">FILM</h2>
            <li v-for="(movie, index) in movies" :key="movie.id + '-' + index">
              <div class="card my-5 text-start border-5 px-5">
                <div class="item">Titolo: {{ movie.title || movie.name }}</div>
                <div class="item">
                  TItolo Originale: {{ movie.original_title }}
                </div>
                <div class="item">
                  <span class="item">Lingua: </span>
                  <img
                    :src="
                      require('@/assets/img/' +
                        movie.original_language +
                        '.png')
                    "
                  />
                </div>
                <div class="item">Voto: {{ movie.vote_average }}</div>
                <div class="item">
                  <img
                    :src="
                      'https://image.tmdb.org/t/p/w342/' + movie.poster_path
                    "
                    :alt="movie.title"
                  />
                </div>
              </div>
            </li>
          </div>
          <div id="serie-tv" class="col-6 border border-black h-100">
            <Series />
            <h2 class="mb-3">SERIE TV</h2>
            <li v-for="(tv, index) in serieTv" :key="tv.id + '-' + index">
              <div class="card my-5 text-start border-5 px-5">
                <div class="item">Titolo: {{ tv.name }}</div>
                <div class="item">TItolo Originale: {{ tv.original_name }}</div>
                <div class="item">
                  <span class="item">Lingua: </span>
                  <img
                    :src="
                      require('@/assets/img/' + tv.original_language + '.png')
                    "
                  />
                </div>
                <div class="item">Voto: {{ tv.vote_average }}</div>
                <div class="item">
                  <img
                    :src="'https://image.tmdb.org/t/p/w342/' + tv.poster_path"
                    :alt="tv.name"
                  />
                </div>
              </div>
            </li>
          </div>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import Search from "@/components/Search.vue";
import Container from "@/components/Container.vue";
import Movies from "@/components/Movies.vue";
import Series from "@/components/Series.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Search,
    Container,
    Movies,
    Series,
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
#Content {
  height: 100vh;
  width: 100%;

  .item {
    margin: 10px 0;
    font-size: 15px;
  }
}

@import "../src/assets/scss/style.scss";
</style>
