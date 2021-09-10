<template>
  <section id="Header">
    <div class="search-bar">
      <input type="text" placeholder="Inserisci titolo..." v-model="input" />
      <button class="button" @click="pressButton"></button>
    </div>
    <div class="results">
      <ul class="all">
        <div class="film">
          <h2>FILM</h2>
          <li v-for="movie in movies" :key="movie.id" class="list">
            <div class="card">
              <ul class="list-pe">
                <div class="item">Titolo: {{ movie.title || movie.name }}</div>
                <div class="item">
                  TItolo Originale: {{ movie.original_title }}
                </div>
                <div class="item">
                  <span> Lingua:</span>
                  <img
                    :src="
                      require('@/assets/img/' +
                        movie.original_language +
                        '.png')
                    "
                  />
                </div>
                <div class="item">Voto:{{ movie.vote_average }}</div>
              </ul>
            </div>
          </li>
        </div>
        <div class="serie-tv">
          <h2>SERIE TV</h2>
          <li v-for="tv in serieTv" :key="tv.id" class="list">
            <div class="card">
              <ul class="list-pe">
                <div class="item">Titolo: {{ tv.name }}</div>
                <div class="item">TItolo Originale: {{ tv.original_name }}</div>
                <div class="item">
                  <span> Lingua:</span>
                  <img
                    :src="
                      require('@/assets/img/' + tv.original_language + '.png')
                    "
                  />
                </div>
                <div class="item">Voto:{{ tv.vote_average }}</div>
              </ul>
            </div>
          </li>
        </div>
      </ul>
    </div>
  </section>
</template>

<script>
import axios from "axios";

export default {
  name: "Header",
  data() {
    return {
      movies: [],
      serieTv: [],
      input: "",
    };
  },
  methods: {
    pressButton() {
      let linkMovie =
        "https://api.themoviedb.org/3/search/movie?api_key=f5d5e3c0ce73a01203b1eaa433c3f0cb&query=" +
        this.input;
      let linkTv =
        "https://api.themoviedb.org/3/search/tv?api_key=f5d5e3c0ce73a01203b1eaa433c3f0cb&query=" +
        this.input;

      axios.get(linkMovie).then((res) => (this.movies = res.data.results));
      axios.get(linkTv).then((res) => (this.serieTv = res.data.results));

      this.input = "";
    },
  },
};
</script>

<style scoped lang="scss">
#Header {
  height: 100vh;
  width: 100%;

  .search-bar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding-bottom: 100px;

    .button {
      height: 20px;
      width: 20px;
      background-color: black;
      cursor: pointer;
    }
  }

  .results {
    display: flex;
    align-items: flex-start;
    justify-content: space-between;
    height: 90vh;
    flex-basis: 100%;

    .all {
      display: flex;
      flex-wrap: wrap;
      justify-content: space-around;
      list-style-type: none;
      height: 100%;
      width: 100%;
      margin: 0;
      padding: 0;

      .list {
        height: 150px;
        width: 100%;
        list-style-type: none;

        .card {
          height: 100%;
          flex-basis: 100%;
          text-align: start;
          background-color: lightblue;
          border: 1px solid black;

          .list-pe {
            margin-top: 20px;

            .item {
              padding-bottom: 8px;
              list-style-type: none;

              img {
                max-width: 35px;
                height: auto;
              }
            }
          }
        }
      }
    }
  }
  .film {
    width: calc((100% / 2) - 2px);
    border: 1px solid black;
  }
  .serie-tv {
    width: calc((100% / 2) - 2px);
    border: 1px solid black;
  }
}
</style>