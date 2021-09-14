<template>
  <div id="card" class="my-5 fs-10">
    <div class="mb-2">
      <img
        :src="'https://image.tmdb.org/t/p/w342/' + item.poster_path"
        :alt="item.title"
      />
    </div>
    <div>Titolo: {{ item.title || item.name }}</div>
    <div>TItolo Originale: {{ item.original_title }}</div>
    <div>
      <span>Lingua: </span>
      <img :src="require('@/assets/img/' + item.original_language + '.png')" />
    </div>
    <div class="voto">
      Valutazione:
      <i
        v-for="n in 5"
        :key="n"
        :class="n <= voteInStar(item.vote_average) ? 'fas' : 'far'"
        class="fa-star"
      ></i>
    </div>
  </div>
</template>

<script>
export default {
  name: "Card",
  props: ["item"],
  methods: {
    voteInStar(vote) {
      return Math.ceil(vote / 2);
    },
  },
};
</script>

<style scoped lang="scss">
#card {
  max-height: 500px;

  img {
    max-height: 450px;
    max-width: 342px;
  }

  .voto i {
    color: goldenrod;
  }
}
</style>