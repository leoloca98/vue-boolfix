<template>
  <section :id="id">
    <h2 class="fs-1 text-uppercase text-white text-center pt-5">
      {{ title }}
    </h2>
    <div class="row p-0 m-0">
      <div
        v-for="item in items"
        :key="item.id"
        class="col-4 d-flex justify-content-center"
      >
        <Card :item="item" />
      </div>
    </div>
    <!-- Results -->
  </section>
</template>

<script>
import Card from "@/components/Card.vue";

export default {
  name: "Results",
  components: {
    Card,
  },
  props: ["title", "items", "id"],
};
</script>

<style lang="scss">
</style>