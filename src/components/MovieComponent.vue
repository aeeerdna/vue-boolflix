<template>
  <!-- container film -->
  <div class="movieContainer">
    <!-- titolo film -->
    <p class="d-flex">
      Title:<span class="ms-2 text-uppercase fw-bold"> {{ movie.title }}</span>
    </p>

    <p class="d-flex">
      Original title:<span class="ms-2 text-uppercase fw-bold">
        {{ movie.original_title }}</span
      >
    </p>

    <p class="d-flex">
      Language:
      <FlagComponent :language="movie.original_language" />
      <span class="ms-2 text-uppercase fw-bold">
        {{ movie.original_language }}</span
      >
    </p>

    <p class="d-flex">
      Vote:<span class="ms-2 text-uppercase fw-bold">
        {{ movie.vote_average }}</span
      >
    </p>
  </div>
</template>

<script>
import FlagComponent from "@/components/FlagComponent.vue";

export default {
  name: "MovieComponent",
  props: {
    movie: Object,
  },
  components: {
    FlagComponent,
  },
};
</script>

<style lang="scss" scoped>
.movieContainer {
  margin-top: 20px;
  border: 2px solid black;
  padding: 10px;
  background-color: lightcoral;

  p {
    line-height: 1.6;
    margin: 0px;
  }
}
</style>
