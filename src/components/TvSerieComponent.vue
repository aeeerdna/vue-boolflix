<template>
  <div class="tvSerieContainer">
    <p class="d-flex">
      Title:<span class="ms-2"> {{ tvSerie.name }}</span>
    </p>

    <p class="d-flex">
      Original title:<span class="ms-2"> {{ tvSerie.original_name }}</span>
    </p>

    <p class="d-flex">
      Language:
      <FlagComponent :language="tvSerie.original_language" />
      <span class="ms-2"> {{ tvSerie.original_language }}</span>
    </p>

    <p class="d-flex">
      Vote:<span class="ms-2"> {{ tvSerie.vote_average }}</span>
    </p>
  </div>
</template>

<script>
import FlagComponent from "@/components/FlagComponent.vue";

export default {
  name: "TvSerieComponent",
  props: {
    tvSerie: Object,
  },
  components: {
    FlagComponent,
  },
};
</script>

<style lang="scss" scoped>
.tvSerieContainer {
  margin-top: 20px;
  border: 2px solid black;
  padding: 10px;
  background-color: lightgreen;

  p {
    line-height: 1.6;
    margin: 0px;
    span {
      text-transform: uppercase;
      font-weight: bold;
    }
  }
}
</style>
